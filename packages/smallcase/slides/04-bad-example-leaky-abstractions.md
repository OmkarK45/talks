# Bad Example: Leaky Abstraction

<div class="grid grid-cols-2 gap-6">

<div>
<div class="text-sm opacity-60 mb-2">The "Message Composer"</div>

```tsx {*}{maxHeight:'300px'}
const MessageComposer = ({
  recipientId,
  threadId,
  onSend,
  apiClient,
  uploadService,
  formatters,
  validators,
  maxAttachments,
  allowedFileTypes,
  maxFileSize,
  mentionUsers,
  emojiData,
  draftsStorage,
  analyticsTracker,
  errorHandler,
  retryConfig,
}) => {
  const [text, setText] = useState('');
  const [attachments, setAttachments] = useState([]);
  const [isSending, setIsSending] = useState(false);
  const [mentions, setMentions] = useState([]);
  
  const handleSend = async () => {
    if (!validators.text(text)) {
      errorHandler.show('Invalid message');
      return;
    }
    
    setIsSending(true);
    analyticsTracker.track('message_started');
    
    try {
      const formatted = formatters.apply(text, mentions);
      const uploaded = await Promise.all(
        attachments.map(f => 
          uploadService.upload(f, { maxSize: maxFileSize })
        )
      );
      
      await apiClient.post(`/threads/${threadId}/messages`, {
        body: formatted,
        attachments: uploaded,
        recipient: recipientId,
      });
      
      draftsStorage.clear(threadId);
      analyticsTracker.track('message_sent');
      onSend();
    } catch (e) {
      errorHandler.handle(e, retryConfig);
    }
    setIsSending(false);
  };
  
  // ... 200 more lines
};
```

</div>

<div v-click>
<div class="text-sm opacity-60 mb-2">Consumer nightmare</div>

```tsx {*}{maxHeight:'300px'}
<MessageComposer
  recipientId={user.id}
  threadId={thread.id}
  onSend={handleMessageSent}
  apiClient={apiClient}
  uploadService={uploadService}
  formatters={messageFormatters}
  validators={messageValidators}
  maxAttachments={5}
  allowedFileTypes={['.png', '.jpg', '.pdf']}
  maxFileSize={10 * 1024 * 1024}
  mentionUsers={teamMembers}
  emojiData={emojiDataset}
  draftsStorage={localDrafts}
  analyticsTracker={analytics}
  errorHandler={toastService}
  retryConfig={{ attempts: 3, delay: 1000 }}
/>

// Want to add GIF support?
// Good luck finding which of the 16 props
// needs to change 🫠

// Writing tests?
// Mock ALL of these. Every. Time.
```

</div>

</div>

