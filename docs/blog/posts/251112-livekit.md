---
date:
  created: 2025-11-12T15:00:00+09:00
  updated: 2025-11-12T15:50:00+09:00
authors:
  - akimovsarvar
categories:
  - Tech Blog
tags:
  - Agent framework
  - Real-time
  - Voice AI
  - WebRTC
---
# LiveKit - One Platform, Real-Time Everything

Video calls need one platform. Live streaming needs another. Voice AI agents need a third. Computer vision processing? That's a fourth vendor. Managing robots remotely? Good luck finding something that works.
LiveKit replaces all of them. One SDK for voice agents, video streaming, vision AI, and robot control. Sub-100ms latency across the board.

<!-- more -->

## What Is LiveKit?

LiveKit is an open-source real-time communication platform built on WebRTC. It's not just another video calling API - it's infrastructure for anything that needs to move audio, video, or data between users and AI agents in real-time.

Voice AI that talks to customers. Video streaming from robots. AI analyzing live camera feeds. Different problems, all in the same session, all using the same platform.

No juggling multiple services. No vendor lock-in. No reinventing WebRTC from scratch.

Beyond video calls, LiveKit replaces: dedicated streaming CDNs, voice AI infrastructure, robotics communication stacks, and complex WebRTC implementations.

---

## How LiveKit Works

**The Stack:**

- **LiveKit Server** - WebRTC SFU (Selective Forwarding Unit) that routes media streams. Self-host or use LiveKit Cloud.
- **Rooms** - Where participants connect. Users, AI agents, robots - all join the same room to communicate.
- **Participants** - Anything connected to a room. Browser clients, mobile apps, backend agents, IoT devices.
- **Tracks** - Audio, video, or data streams published by participants. Subscribe to tracks you want to receive.

**Simple flow:**

1. Server creates a room
2. Participants join with access tokens
3. Publish tracks (camera, mic, screen, data)
4. Subscribe to other participants' tracks
5. Server forwards media directly between participants

```python
# Backend: Create room and generate token
room = await livekit_api.room.create_room("my-room")
token = create_token(identity="user1", room_name="my-room")

# Client: Join and publish
room = Room()
await room.connect(url, token)
await room.local_participant.publish_track(camera_track)

```

**No central transcoding** = Server doesn't decode/re-encode video. Server just forwards packets directly. Low latency, scales horizontally.

**Agent workers** sit between server and AI models. Join rooms as participants, process audio/video, call AI APIs, publish responses back.

📚 [Architecture overview](https://docs.livekit.io/home/get-started/intro-to-livekit/#livekit-ecosystem)

---

## Build Voice AI That Actually Works

**Replaces:** Custom STT-LLM-TTS pipelines, latency-prone API chains, fragile state management

You know the drill with voice AI: chain together separate APIs for speech-to-text, your LLM, and text-to-speech. Each step adds 300ms of latency. User interrupts mid-sentence? Your state management explodes. Your app crashes overnight because the TTS API went down.

**LiveKit Agents:**

```python
from livekit.agents import VoiceAssistant
from livekit.plugins import openai, deepgram, elevenlabs

assistant = VoiceAssistant(
    stt=deepgram.STT(),
    llm=openai.LLM(model="gpt-4"),
    tts=elevenlabs.TTS(),
)
assistant.start(room)

```

Your voice AI is live. Natural interruptions handled automatically. Turn detection using transformer models. Multi-agent workflows when you need them.

**ChatGPT's Advanced Voice Mode?** Built on LiveKit. Millions of users, every day.

Building a phone-based customer service bot? Restaurant ordering system? Medical triage assistant? One framework, production-ready from day one.

📚 [Voice AI quickstart](https://docs.livekit.io/agents/) · [Agent examples](https://github.com/livekit/agents/tree/main/examples)

---

## Stream Video Without the Video Streaming Complexity

**Replaces:** Traditional CDNs, HLS delays, separate chat infrastructure

Setting up HLS streaming: 10-30 seconds of latency, viewers see different things at different times, separate WebSocket server for chat, separate RTMP ingest pipeline, separate viewer analytics.

**LiveKit's WebRTC Streaming:**

```python
room = Room()
await room.connect(url, token)

# Start streaming
await room.local_participant.publish_track(video_track)

```

Every viewer is within 250ms of real-time. They all see the same frame at the same moment. Two-way audio/video built-in - any viewer can become a streamer instantly. Chat and data messages included. Record sessions with one API call.

📚 [Livestreaming docs](https://livekit.io/use-cases/livestreaming) · [Recording guide](https://docs.livekit.io/home/egress/overview/)

---

## Control Robots From Anywhere

**Replaces:** Custom video streaming solutions, high-latency feeds, unreliable connections

Your robots have cameras. Sensors. Microphones. You need that data streamed to operators in real-time, or processed by AI in the cloud, or both. Building this from scratch means dealing with video encoding, network resilience, secure streaming, and somehow doing it all with under 100ms latency.

**LiveKit for Robotics:**

```python
# On the robot
track = VideoTrack.from_camera()
room.local_participant.publish_track(track)

# Send sensor data
await room.local_participant.publish_data(
    sensor_readings,
    destination_identities=["operator"]
)

```

Stream from thousands of robots. Route specific feeds to operators. Process video with AI models in real-time. All over unreliable mobile networks - WebRTC handles packet loss, adapts bitrate automatically.

Agricultural robots working in fields with spotty connection? WebRTC stays connected where traditional streaming dies.

📚 [Robotics use case](https://livekit.io/use-cases/robotics) · [Data streams guide](https://docs.livekit.io/home/client/data/overview/)

---

## Mix Humans and AI in the Same Call

**Replaces:** Separate platforms, awkward transfers, repeating your problem three times

Customer calls. AI greets and troubleshoots. Needs billing help. Transfer. Customer explains issue again. Needs technical support. Transfer again. Explain everything from scratch. Again.

**LiveKit Multi-Agent Workflows:**

```python
class FrontlineAgent(Agent):
    @function_tool()
    async def transfer_to_billing(self):
        return BillingAgent(chat_ctx=self.chat_ctx)

    @function_tool()
    async def escalate_to_human(self):
        return HumanAgent(chat_ctx=self.chat_ctx)

# chat_ctx = full conversation history passes to next agent

```

AI greeter → Billing AI → Human specialist. Same call. Full context preserved. No repeating. Each agent knows what previous agents discussed.

**Examples:** Medical triage (symptoms → specialist), drive-thru ordering (greeter → order taker → payment), call centers (AI screens → human closes).

📚 [Multi-agent workflows](https://docs.livekit.io/agents/build/workflows/) · [Agent handoff examples](https://github.com/livekit/agents/tree/main/examples)

---

## Actually Multimodal AI

**Replaces:** Voice-only AI, separate video processing pipelines

Your AI should see what users see. Point a camera at a product, ask questions about it. Share your screen, get help with what you're looking at. Current solution: send screenshots to vision models, dealing with terrible latency.

**LiveKit Vision Agents:**

```python
assistant = MultimodalAgent(
    video=True,  # Agent can see
    audio=True,  # Agent can hear
    llm=openai.LLM(model="gpt-4o"),
)

# Camera feed goes directly to the agent
# User speaks, agent sees and responds

```

**Gemini Live agents that can see**. Vision-enabled customer support. AI assistants for virtual events that understand what's on screen. Educational apps where AI tutors watch students solve problems.

Video, audio, and data - all in one real-time session with your AI models.

📚 [Vision agent example](https://github.com/livekit/agents/tree/main/examples) · [Multimodal capabilities](https://docs.livekit.io/agents/integrations/)

---

## Deploy Anywhere

**Replaces:** Vendor lock-in, inflexible hosting

**Self-Hosted:**

```bash
# Install LiveKit Server (Linux)
curl -sSL https://get.livekit.io | bash

# Run it
livekit-server --dev

```

Full control. Your infrastructure. Your compliance requirements. Apache 2.0 license - modify whatever you need.

---

## Get Started

**Try it live:** Visit [kitt.livekit.io](https://kitt.livekit.io/) - talk to a real-time voice AI agent. Running on LiveKit. All open source. Just hit the Connect button at top-right.

**Quick Start (Python):**

```bash
pip install livekit livekit-agents

# Create your first voice agent
python agent.py dev

```

**Quick Start (Self-Hosted):**

```bash
docker run -p 7880:7880 \
  -e LIVEKIT_KEYS="devkey: secret" \
  livekit/livekit-server:latest --dev

```

10 minutes to working prototype. Zero maintenance. Unlimited possibilities.

---

## Real-World Examples

**Voice AI:** Customer service bots that handle thousands of concurrent calls
**Live Shopping:** Interactive auctions with millions in sales

**Computer Vision:** Real-time face detection for attendance systems - process camera feeds, draw bounding boxes, stream annotated video to monitoring dashboards

**Robotics:** Controlling drones or agricultural machines with real-time video and telemetry

**Education:** Virtual classrooms with breakout rooms and screen sharing

**Events:** Interactive livestreams with real-time Q&A

**One platform. Every real-time use case.**

---

## Resources

📖 [Documentation](https://docs.livekit.io/)

💻 [GitHub](https://github.com/livekit/livekit)

🎓 [Free Course (DeepLearning.AI)](https://www.deeplearning.ai/)

🔧 [Example Agents](https://github.com/livekit-examples/python-agents-examples)

Start building: [livekit.io](https://livekit.io/)
