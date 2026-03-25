---
title: "Voice Input"
description: "Use your voice to interact with AI tools — faster capture, more natural explanations, less friction."
weight: 15
---

# Voice Input

Most AI tools accept text input, but for many tasks — especially explaining processes, thinking out loud, or capturing quick notes — speaking is faster and more natural than typing. Voice input reduces the friction of getting your thoughts into the AI, and tends to produce more conversational, less self-edited raw material.

## When to Use

- You're documenting a process you know well and can explain faster than you can type. See the [SOP / Process Documentation](../playbooks/sop-process-documentation.md) playbook.
- You want to capture a quick journal entry or reflection without switching to a keyboard. See the [Automated Journaling](../playbooks/automated-journaling.md) playbook.
- You're working through a problem out loud and want the AI to engage with your thinking in real time.
- You're on the go and want to capture something before you lose it.

## Platform Voice Support

### Claude

- **Mobile app (iOS/Android)** — Full voice mode available on all plans (free and paid). Supports voice input and output with multiple voice personalities. English only. Tap the microphone icon to start.
- **Claude Code CLI** — Voice dictation via the `/voice` command. Push-to-talk: hold spacebar, speak, release. Requires v2.1.69+ and a Claude.ai account. Currently in limited rollout. Supports 20 languages.
- **Desktop / Web** — Voice mode is in gradual rollout and not yet broadly available.

### ChatGPT

- **Mobile app (iOS/Android)** — Advanced Voice Mode uses GPT-4o to process audio directly. Supports video and screen sharing during voice conversations. Available to Plus, Pro, and Team users; free users get a monthly preview.
- **Web app (chatgpt.com)** — Voice mode available to all logged-in users.
- **Windows desktop app** — Voice mode supported.
- **macOS desktop app** — Voice mode was retired in January 2026.

### Ollama (Local Models)

Ollama has no native voice support. Voice input requires combining a speech-to-text tool with Ollama:

- **Typical stack:** Whisper (STT) → Ollama (LLM) → pyttsx3 or Bark (TTS)
- **Notable open-source projects:**
  - [ollama-voice](https://github.com/maudoin/ollama-voice) — Whisper + Ollama + pyttsx3, fully offline
  - [local-talking-llm](https://github.com/vndee/local-talking-llm) — Whisper + Ollama + Bark, no internet required
- All options require manual setup (Python, model downloads, etc.)

## Tips

- Talk like you're explaining something to a colleague, not dictating a document. The AI can clean up the structure later.
- Don't worry about filler words, restarts, or imperfect grammar — transcription tools and AI are both good at handling natural speech.
- For longer explanations, pause between logical sections. This makes it easier to review and edit the transcript afterward.
