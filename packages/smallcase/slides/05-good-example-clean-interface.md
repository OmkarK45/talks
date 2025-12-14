# Good Example: Clean Interface

<div class="grid grid-cols-2 gap-6">

<div>
<div class="text-sm opacity-60 mb-2">Composed from focused pieces</div>

```tsx {*}{maxHeight:'280px'}
const MessageComposer = ({ threadId, onSend }) => {
  const { send, isSending } = useMessages(threadId);
  
  return (
    <ComposerProvider threadId={threadId}>
      <TextEditor />
      <AttachmentPicker />
      <MentionSuggestions />
      <EmojiPicker />
      <SendButton 
        onSend={async (content) => {
          await send(content);
          onSend();
        }}
        disabled={isSending}
      />
    </ComposerProvider>
  );
};
```

<div class="mt-4 text-sm opacity-60">Each piece does one thing well</div>

```tsx
// TextEditor - just text editing
// AttachmentPicker - just file selection
// useMessages - just API communication
// ComposerProvider - just shared state
```

</div>

<div v-click>
<div class="text-sm opacity-60 mb-2">Consumer happiness</div>

```tsx
<MessageComposer 
  threadId={thread.id}
  onSend={handleSent}
/>

<ComposerProvider threadId={thread.id}>
  <TextEditor />
  <CustomGifPicker />  
  <AttachmentPicker accept=".pdf" />
  <SendButton onSend={send} />
</ComposerProvider>
```

<div class="mt-6 grid grid-cols-2 gap-3">
  <div class="p-3 rounded-lg bg-green-500/10 border border-green-500/30 text-sm">
    <span class="text-green-400">✓</span> 2 props vs 16
  </div>
  <div class="p-3 rounded-lg bg-green-500/10 border border-green-500/30 text-sm">
    <span class="text-green-400">✓</span> Composable
  </div>
  <div class="p-3 rounded-lg bg-green-500/10 border border-green-500/30 text-sm">
    <span class="text-green-400">✓</span> Easy to test
  </div>
  <div class="p-3 rounded-lg bg-green-500/10 border border-green-500/30 text-sm">
    <span class="text-green-400">✓</span> Easy to extend
  </div>
</div>

</div>

</div>

