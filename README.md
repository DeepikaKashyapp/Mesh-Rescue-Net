📡 EchoChat: The Off-Grid Emergency Bridge
Smarter Rescue. Zero Infrastructure.

EchoChat is a decentralized, offline communication system designed for disaster zones where cellular towers have failed. Unlike standard mesh apps, EchoChat features "Urgency Intelligence"—a custom protocol that prioritizes life-saving SOS alerts over routine status updates, ensuring medical help arrives first.

🚨 The Problem
During natural disasters (floods, landslides, earthquakes), cellular infrastructure often fails, isolating victims from rescuers. Existing off-grid solutions operate on a "First-In, First-Out" basis, meaning a critical "Heart Attack" SOS can get stuck behind hundreds of "I'm safe" messages in a congested network.

💡 The Solution: Urgency Intelligence
EchoChat transforms standard smartphones into a resilient mesh network.

Zero-Infrastructure: Works 100% offline using Bluetooth LE and Wi-Fi Direct.

Priority Triage Protocol: A smart algorithm that assigns a "Priority Level" (0-5) to every packet. If the network buffer exceeds 80%, it automatically drops low-priority traffic to ensure SOS signals have zero latency.

Privacy Preserved: Messages "hop" through stranger's phones using Libsodium End-to-End Encryption. Relay nodes forward encrypted data without being able to read it.

⚙️ System Architecture
1. The Tech Stack
Language: Kotlin (Native Android)

Connectivity: Google Nearby Connections API (Strategy.P2P_CLUSTER)

Security: Libsodium (Curve25519 Key Exchange + XSalsa20 Encryption)

Local DB: SQLite (for offline message persistence)

Cloud Gateway: Supabase/PostgreSQL (for syncing when internet is found)

2. The Triage Algorithm (The "Brain")
The network congestion logic follows a strict hierarchy:

Level 0 (Critical): Medical SOS, Fire, Life-Threatening (Never Dropped).

Level 1 (Urgent): Rescue Team Coordination.

Level 2 (Routine): "I am safe" Status Updates.

Congestion Rule: If Buffer > 80%, drop all Level > 1. If Buffer = 100% SOS, drop Oldest SOS (Freshness Eviction).

🔒 Security Implementation
We implement Hybrid Encryption to ensure privacy in the mesh:

Key Exchange: We use Elliptic Curve Cryptography (Curve25519) to generate a Shared Secret between two devices without transmitting keys.

Stream Encryption: We use XSalsa20 (XOR-based) to encrypt the actual message payload.

Anonymity: Intermediate Relay Nodes see only the TargetID and Ciphertext. They act as blind couriers.

🚀 Installation & Setup
Prerequisites
Android Studio Iguana or newer.

Minimum SDK: 26 (Android 8.0).

Two or more Android devices (Emulator support for Bluetooth is limited).

Steps
Clone the Repo:

Bash
git clone https://github.com/YourUsername/EchoChat-Mesh.git
Open in Android Studio: Allow Gradle to sync dependencies (including lazysodium-android).

Permissions: On first launch, you MUST grant "Nearby Devices" and "Location" permissions when prompted.

Build & Run: Deploy to 2+ physical devices to test the mesh.

📱 How to Demo (For Judges)
Scenario 1: The "Flood" Test (Congestion)
Connect 2 phones.

Tap the "Simulate Flood" button (Red).

Observe the "Network Buffer" bar fill up.

Send a "Critical SOS".

Result: The buffer clears the spam, and the SOS arrives instantly.

Scenario 2: The "Blind Relay" (Privacy)
Setup: Phone A -> Phone B -> Phone C.

On Phone A, select "Private Mode" and enter Phone C's ID.

Send "Secret Message".

Result: Phone B's logs show "Relaying Encrypted Packet..." (Payload is unreadable). Phone C receives the decrypted text.

🔮 Future Roadmap
Drone Relays: Mounting Gateway Nodes on drones to bridge distant clusters.

Voice-to-Text SOS: NLP for injured victims who cannot type.

B2G Integration: API integration with NDRF/SDMA for national disaster response.

## 👥 Team & Contributions

* **Deepak Kr Singh:** Core Infrastructure & Connectivity. Designed the multi-hop routing architecture, optimized battery-efficient device discovery utilizing Bluetooth Low Energy (BLE) and Wi-Fi Direct, and implemented Time-to-Live (TTL) packet control to prevent infinite message loops within the mesh.
* **Deepika Kashyap:** Urgency Intelligence & Protocol Design. Engineered the core functional logic and custom priority triage algorithm. Designed and implemented the packet-dropping protocol based on message urgency levels, ensuring zero-latency routing for critical SOS alerts over routine data.
