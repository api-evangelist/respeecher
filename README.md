# Respeecher (respeecher)

Respeecher is an AI voice company known for high-fidelity speech-to-speech (STS) voice conversion and text-to-speech (TTS), widely used across film, television, games, and advertising. It exposes two documented, self-service public APIs plus a bespoke enterprise service.

- **Voice Marketplace API** (`https://gateway.respeecher.com`) — request/response REST with a downloadable OpenAPI 3.0.2 spec (`/api/openapi.json`, "Voice Marketplace API 0.6.0", 38 paths). Secured with an `api-key` header; keys are generated at `marketplace.respeecher.com/account`. Covers voices, speech-to-speech conversion orders, text-to-speech, calibration, recordings, projects/folders, credits, and statistics.
- **Respeecher Space Real-Time TTS API** (`https://api.respeecher.com/v1/public/tts/{en-rt,ua-rt}`) — low-latency real-time text-to-speech that starts streaming audio in under 200ms via three transports: one-shot `POST /tts/bytes`, HTTP SSE (`POST /tts/sse`), and a bidirectional **WebSocket** channel (`wss://api.respeecher.com/v1/public/tts/en-rt`). Authenticated with `X-API-Key` (or an `api_key` query parameter for browser WebSocket clients). Official Python and TypeScript SDKs; LiveKit, Pipecat, Ultravox, and VAPI integrations.
- **AI Voice Lab** — a white-glove, per-project enterprise service for custom voice cloning (studios/enterprises); contact-sales, not a public API.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/respeecher/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/respeecher/refs/heads/main/apis.yml)

## Access Model

Both APIs are **self-service** — create an API key and pay as you go (prepaid credits or subscriptions on the Marketplace, ~$2/hour usage-based on the real-time Space API). No partner gating is required for the documented endpoints. Enterprise AI Voice Lab work is negotiated separately.

## Tags

- Voice AI
- Voice Cloning
- Speech to Speech
- Text to Speech
- Voice Conversion
- Real Time
- Media and Entertainment

## Timestamps

- **Created:** 2026-07-11
- **Modified:** 2026-07-11

## APIs

### Respeecher Voices API

List, search, favorite, and configure the marketplace catalog of AI voices (`GET /api/v2/voices`, `/api/v2/voices/search`, `/api/v2/voices/settings`) plus accent and narration-style samples. Voices filter by gender, age, pitch, nationality, species, and visibility.

- **Base URL:** `https://gateway.respeecher.com`
- [Documentation](https://docs.respeecher.com/) · [API Reference](https://docs.respeecher.com/endpoints-reference/) · [OpenAPI](openapi/respeecher-openapi.yml)

### Respeecher Speech-to-Speech Conversion API

Create and retry speech-to-speech voice conversion jobs that transform an uploaded recording into a target marketplace voice with accent and semitone pitch control (`POST /api/v2/orders`, `/api/recordings/conversion-order`, `POST /api/v2/orders/retry/{recording_id}`).

- **Base URL:** `https://gateway.respeecher.com`
- [Documentation](https://www.respeecher.com/speech-to-speech) · [API Reference](https://docs.respeecher.com/endpoints-reference/) · [OpenAPI](openapi/respeecher-openapi.yml)

### Respeecher Text-to-Speech API

Generate speech from text using 150+ narration styles on the Voice Marketplace (`POST /api/v2/recordings/tts`, `GET /api/tts-voices`). A dedicated [Python client](https://github.com/respeecher/respeecher_tts) wraps this endpoint.

- **Base URL:** `https://gateway.respeecher.com`
- [Documentation](https://www.respeecher.com/api) · [API Reference](https://docs.respeecher.com/endpoints-reference/) · [OpenAPI](openapi/respeecher-openapi.yml)

### Respeecher Calibration API

Create, list, enable, and delete voice calibrations that determine the mean pitch of a source voice for better pitch matching during conversion (`POST /api/calibration`, `POST /api/calibration/auto`, `PUT /api/calibration/{calibration_id}/enable`).

- **Base URL:** `https://gateway.respeecher.com`
- [API Reference](https://docs.respeecher.com/endpoints-reference/) · [OpenAPI](openapi/respeecher-openapi.yml)

### Respeecher Recordings API

Upload, list, update, export, and delete original recordings and their conversions in WAV, OGG, MP3, and FLAC (`GET/POST /api/recordings`, `/api/recordings/originals`, `/api/recordings/conversions`, `/api/recordings/export`), with per-recording notes and metadata.

- **Base URL:** `https://gateway.respeecher.com`
- [API Reference](https://docs.respeecher.com/endpoints-reference/) · [OpenAPI](openapi/respeecher-openapi.yml)

### Respeecher Projects and Folders API

Organize recordings and conversions into projects and folders with pagination, filtering, ZIP export, and statistics (`GET/POST /api/projects`, `/api/folders`, `GET /api/projects/{project_id}/export`, `/api/stats`).

- **Base URL:** `https://gateway.respeecher.com`
- [API Reference](https://docs.respeecher.com/endpoints-reference/) · [OpenAPI](openapi/respeecher-openapi.yml)

### Respeecher Credits API

Check the account credit balance that meters marketplace TTS and STS usage (`GET /api/credits`).

- **Base URL:** `https://gateway.respeecher.com`
- [API Reference](https://docs.respeecher.com/endpoints-reference/) · [OpenAPI](openapi/respeecher-openapi.yml)

### Respeecher Space Real-Time TTS API

Low-latency real-time text-to-speech that begins streaming audio in under 200ms via one-shot bytes (`POST /tts/bytes`, up to ~5,000 characters), HTTP SSE (`POST /tts/sse`), and a bidirectional WebSocket channel (`wss://api.respeecher.com/v1/public/tts/en-rt`, `GET /tts/websocket`) keyed by `context_id`. English (`en-rt`) and Ukrainian (`ua-rt`) models; `X-API-Key` auth; official Python and TypeScript SDKs; LiveKit, Pipecat, Ultravox, and VAPI integrations.

- **Base URL:** `https://api.respeecher.com/v1/public/tts/en-rt`
- [Documentation](https://space.respeecher.com/docs/quickstart) · [WebSocket Reference](https://space.respeecher.com/docs/api/tts/web-socket) · [AsyncAPI](asyncapi/respeecher-asyncapi.yml)

## Common Properties

- [LinkedIn](https://www.linkedin.com/company/respeecher)
- [Website](https://www.respeecher.com)
- [Voice Marketplace API Docs](https://docs.respeecher.com/)
- [Space Real-Time TTS Docs](https://space.respeecher.com/docs)
- [Sign Up / API Keys](https://marketplace.respeecher.com/account)
- [Plans](plans/respeecher-plans-pricing.yml)
- [Rate Limits](rate-limits/respeecher-rate-limits.yml)
- [Fin Ops](finops/respeecher-finops.yml)
- [OpenAPI](https://gateway.respeecher.com/api/openapi.json)
- [Blog](https://www.respeecher.com/blog)

## Review

Does Respeecher expose a documented public WebSocket API? **Yes.** The Respeecher Space real-time TTS API publishes a bidirectional WebSocket endpoint (`wss://api.respeecher.com/v1/public/tts/{en-rt,ua-rt}`), documented alongside SSE and one-shot bytes transports, and Respeecher publishes its own AsyncAPI 2.6.0 for the WebSocket channels. See [`review.yml`](review.yml) and the authored [`asyncapi/respeecher-asyncapi.yml`](asyncapi/respeecher-asyncapi.yml).

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
