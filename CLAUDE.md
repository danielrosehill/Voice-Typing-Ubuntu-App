# Voice Typing Ubuntu App - Project Context

## Project Overview

This is a voice-to-text/dictation application for Ubuntu Linux that provides OS-level speech-to-text integration. The app uses cloud-based STT APIs (starting with Deepgram) rather than local inference, and must work system-wide on Wayland.

**Status**: Work in progress, built in public from initial stages

**Base**: Started from [Deepgram's voice-keyboard-linux](https://github.com/deepgram/voice-keyboard-linux) starter project

## User Context & Motivation

Daniel is a power user of voice typing who has spent a year using various STT solutions. Key insights:

- **Primary input method**: Voice typing has become his default workflow after extensive testing
- **Cloud API preference**: Deliberately choosing cloud STT over local inference for quality and consistency
- **OS-level integration required**: Apps with built-in dictation create gaps; needs to work everywhere
- **Wayland compatibility critical**: Must type into any window/field on Wayland (this is a known challenge)

## Technical Environment

- **OS**: Ubuntu 25.10 with KDE Plasma on Wayland
- **Hardware**: AMD Radeon RX 7700 XT GPU (but not using local inference)
- **Audio**: PipeWire audio system
- **Input**: Uses HID USB button mapped to F13 for activation
- **Timezone**: IST/IDT (UTC+2/+3)

## MVP Feature Requirements (Priority Order)

### 1. Hotkey Support
- User-configurable hotkey selection (default: F13)
- Settings must persist between sessions
- **Default mode**: "Tap tap" - tap once to start, tap again to stop
- **Optional mode**: PTT (push-to-talk) - hold to type
- **Advanced option**: Separate stop button for two-pedal operation

### 2. Microphone Handling
- User selects microphone from available devices
- Selection persists across sessions
- Store config in local device storage

### 3. Model Selection
- **Initial scope**: Deepgram only
- **Future vision**: Support multiple cloud providers (Whisper, Speechmatics, etc.)
- Note: Each provider integration adds complexity, so starting minimal

### 4. GUI
- Simple interface for start/stop and settings configuration
- **Default behavior**: Dock to system tray
- Must be recallable and closeable from tray
- Clean, minimal design

### 5. Type Anywhere
- **CRITICAL SUCCESS CRITERION**: Must type wherever cursor is positioned
- Must work across all applications on Wayland
- This is non-negotiable - the app is useless without this

### 6. API Spend Monitoring
- Display current API spending
- User-specific API key configuration
- **Update frequency**: Polling every hour is sufficient
- **Initial scope**: Simple dollar display
- **Future additions**: Daily caps, spend warnings, alerts

## Future Features (Not MVP)

### Planned Enhancements
1. **Mic level monitoring**: dB display with alerting for low/clipping levels
2. **Post-processing**: Especially useful for async/note-taking mode
3. **Custom dictionary**: User-defined replacements and corrections
4. **Long-form STT**: Separate from real-time, with chunking strategy

### Non-Features (Explicitly Out of Scope)
1. VAD / always-on listening
2. Wake word activation (at least initially)
3. Local inference (cloud API is the design choice)

## Development Philosophy

- **Incremental iteration**: Break tasks into small chunks
- **Feature complete over feature rich**: Get core functionality solid first
- **Real-world testing**: Daniel will use this daily, so reliability matters
- **Build in public**: Sharing progress from early stages

## API & Integration Notes

- **Primary provider**: Deepgram (real-time STT with excellent on-the-fly punctuation)
- **API key storage**: Local, persistent, user-specific
- **Cost awareness**: Spend monitoring is essential for Daniel's confidence in daily use
- **Future consideration**: Replicate recently added Whisper to their offering

## Key Technical Challenges

1. **Wayland text injection**: Many STT apps fail here - this is the critical technical hurdle
2. **Persistent configuration**: Hotkey, mic selection, API keys must survive restarts
3. **System tray integration**: Need proper KDE Plasma tray docking
4. **Audio device handling**: PipeWire device selection and routing
5. **API cost tracking**: Accurate spend monitoring without excessive polling

## Testing & Validation

When working on this project:
- Test text injection in multiple applications (terminal, text editor, browser, etc.)
- Verify Wayland compatibility specifically
- Test hotkey detection with F13 and other keys
- Ensure settings persistence across application restarts
- Validate microphone selection works with PipeWire
- Test system tray functionality in KDE Plasma

## Related Context

Daniel has extensive experience with:
- Various STT models and providers (Deepgram, Whisper, Speechmatics)
- Both real-time and async transcription workflows
- Local GPU inference (but prefers cloud for this use case)
- Audio setup troubleshooting on Linux/PipeWire
- Python development with conda/venv environments

## Development Environment Notes

- Likely using Python with conda/venv
- May use existing conda environments rather than creating new ones
- Virtual environment typically at `.venv` (git-ignored)
- Will version control and push to GitHub frequently
- Expect repo to be private initially

## Communication Preferences

- Assume technical competence - no need to oversimplify
- Focus on actionable information over lengthy explanations
- Fix obvious issues (security, outdated syntax) proactively
- Ask for clarification if requirements are ambiguous
- Document technical decisions but only when explicitly requested
