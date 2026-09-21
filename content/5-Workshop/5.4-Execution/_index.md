---
title: "Program Execution"
date: 2026-06-01
weight: 4
chapter: false
pre: " <b> 5.4. </b> "
---

### 1. User Login, Registration & Email Verification via Amazon SES

The platform enforces secure authentication backed by HTTPS in-transit encryption and SSL certificates provisioned through AWS Certificate Manager. Users can log into existing accounts or register a new identity, receiving verification emails dispatched automatically through Amazon Simple Email Service:

1. Open a web browser and navigate to the official production URL: **[https://ericmai.io.vn](https://ericmai.io.vn)**.
2. Verify the padlock SSL security icon on the address bar and log in using configured credentials.
3. During registration or password recovery, the backend triggers Amazon SES to dispatch verification OTP codes directly to the user's Gmail inbox.

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.4-Execution/login.jpg" alt="ChatPulse Login and Authentication Screen" style="max-width: 100%; height: auto; border-radius: 8px; box-shadow: 0 4px 16px rgba(0,0,0,0.12); border: 1px solid #e2e8f0;" />
  <p style="font-size: 0.9rem; color: #64748b; margin-top: 8px; font-style: italic;">Figure 5.26: User login and authentication portal rendered at domain ericmai.io.vn</p>
</div>

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.4-Execution/register.jpg" alt="User Registration Interface" style="max-width: 100%; height: auto; border-radius: 8px; box-shadow: 0 4px 16px rgba(0,0,0,0.12); border: 1px solid #e2e8f0;" />
  <p style="font-size: 0.9rem; color: #64748b; margin-top: 8px; font-style: italic;">Figure 5.27: User registration completion modal on the ChatPulse platform</p>
</div>

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.4-Execution/verification_gmail.jpg" alt="Email verification message from Amazon SES" style="max-width: 100%; height: auto; border-radius: 8px; box-shadow: 0 4px 16px rgba(0,0,0,0.12); border: 1px solid #e2e8f0;" />
  <p style="font-size: 0.9rem; color: #64748b; margin-top: 8px; font-style: italic;">Figure 5.28: Gmail inbox displaying the automated email verification message dispatched via Amazon SES</p>
</div>

---

### 2. Friend Management & User Profile Search

Directory management capabilities empower users to discover connections via phone number, inspect user profile attributes, and manage friendships:

1. **Search users by phone number:** Enter a phone number in the search bar to query accounts with instant real-time results.
2. **Inspect user profile card:** Click on the search result to display the profile card containing user avatar, bio, phone number, gender, and date of birth, along with options to block or unblock the user.
3. **Synchronize real-time online presence:** Once connected as friends, online presence indicators display a vibrant green dot immediately, synchronized through the Redis in-memory cache with sub-15ms round-trip latency.

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.4-Execution/profile_friend.jpg" alt="User search by phone and profile inspection card" style="max-width: 100%; height: auto; border-radius: 8px; box-shadow: 0 4px 16px rgba(0,0,0,0.12); border: 1px solid #e2e8f0;" />
  <p style="font-size: 0.9rem; color: #64748b; margin-top: 8px; font-style: italic;">Figure 5.29: User search by phone number displaying profile attributes including avatar, bio, phone, gender, date of birth, and block or unblock controls</p>
</div>

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.4-Execution/list_friend.jpg" alt="Friend list with real-time presence indicators" style="max-width: 100%; height: auto; border-radius: 8px; box-shadow: 0 4px 16px rgba(0,0,0,0.12); border: 1px solid #e2e8f0;" />
  <p style="font-size: 0.9rem; color: #64748b; margin-top: 8px; font-style: italic;">Figure 5.30: Friend list directory with real-time online status indicators synchronized via Redis</p>
</div>

---

### 3. Real-Time Messaging, Image & File Sharing

The real-time communications layer forms the backbone of ChatPulse, built upon WebSocket Socket.io bidirectional channels integrated with Amazon S3 cloud object storage:

1. **Instant text messaging:** Exchange messages between active users with instantaneous delivery and zero page refreshes, confirming sent and delivered receipts.
2. **Secure file uploads:** The client requests a short-lived S3 Pre-signed URL from the backend and transmits payloads directly to the Amazon S3 Bucket, ensuring optimal upload speed and removing bandwidth bottlenecks from the EC2 host.
3. **Document exchange and storage:** The platform demonstrates direct transmission of a PDF document within the active dialogue stream, allowing users to preview or download the file safely while storing the uploaded file object securely inside Amazon S3.

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.4-Execution/messages_real-time_upload_file.jpg" alt="Real-time messaging dialogue with PDF file attachment" style="max-width: 100%; height: auto; border-radius: 8px; box-shadow: 0 4px 16px rgba(0,0,0,0.12); border: 1px solid #e2e8f0;" />
  <p style="font-size: 0.9rem; color: #64748b; margin-top: 8px; font-style: italic;">Figure 5.31: Live conversation view displaying real-time text dialogue and an attached PDF document</p>
</div>

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.4-Execution/bucket_file.jpg" alt="Amazon S3 Bucket storing uploaded file objects" style="max-width: 100%; height: auto; border-radius: 8px; box-shadow: 0 4px 16px rgba(0,0,0,0.12); border: 1px solid #e2e8f0;" />
  <p style="font-size: 0.9rem; color: #64748b; margin-top: 8px; font-style: italic;">Figure 5.32: Amazon S3 Bucket securely storing uploaded file objects from the ChatPulse application</p>
</div>

---

### 4. WebRTC Voice & Video Calling via LiveKit SFU

The platform integrates enterprise-grade WebRTC through a dedicated LiveKit Selective Forwarding Unit (SFU), delivering high-definition peer-to-peer audiovisual streams with ultra-low latency:

1. **Initiate call session:** Users click the voice call or video call icon directly within an active conversation to establish connection.
2. **Incoming and dialing screens:** The caller interface displays dialing status while the recipient receives an incoming call modal dialogue with ring tone notifications.
3. **High-definition two-way video room:** Upon handshake completion, the interface launches an immersive full-screen call room displaying camera feeds from both participants with sub-150ms transmission latency and crisp audio synchronization.
4. **In-call controls:** Participants can toggle microphone muting, disable or enable camera streams, switch media devices, and disconnect cleanly.

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.4-Execution/calling.jpg" alt="Outbound call initiation screen" style="max-width: 100%; height: auto; border-radius: 8px; box-shadow: 0 4px 16px rgba(0,0,0,0.12); border: 1px solid #e2e8f0;" />
  <p style="font-size: 0.9rem; color: #64748b; margin-top: 8px; font-style: italic;">Figure 5.33: Outbound calling screen displaying recipient identity and dialing connection state</p>
</div>

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.4-Execution/in_call.jpg" alt="Active WebRTC video call session" style="max-width: 100%; height: auto; border-radius: 8px; box-shadow: 0 4px 16px rgba(0,0,0,0.12); border: 1px solid #e2e8f0;" />
  <p style="font-size: 0.9rem; color: #64748b; margin-top: 8px; font-style: italic;">Figure 5.34: Active full-screen two-way WebRTC video call room with real-time video and audio transmission</p>
</div>

---

### 5. Intelligent AI Assistant & Amazon Polly Voice Accessibility

ChatPulse elevates conversational collaboration by combining generative language models with scalable cloud speech synthesis:

1. **Conversational AI interaction:** Users can submit inquiries or ask for automated assistance directly inside the chat window. The backend relays prompts to large language models, returning coherent and intelligent guidance directly within the conversation thread.
2. **Text-to-Speech narration via Amazon Polly:**
   - A dedicated audio speaker icon is embedded beside each message bubble.
   - Clicking the speaker triggers an authenticated API request to **Amazon Polly** on AWS.
   - Amazon Polly synthesizes natural, human-like speech streams in Vietnamese and English, playing audio playback directly in the browser to support accessibility and hands-free listening.

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.4-Execution/polly.jpg?v=2" alt="AI assistant interaction and Amazon Polly voice narration" style="max-width: 100%; height: auto; border-radius: 8px; box-shadow: 0 4px 16px rgba(0,0,0,0.12); border: 1px solid #e2e8f0;" />
  <p style="font-size: 0.9rem; color: #64748b; margin-top: 8px; font-style: italic;">Figure 5.35: AI Assistant prompt dialogue and speech synthesis narration powered by Amazon Polly</p>
</div>

---

### 6. Application Video Demo

Below is the video demonstration walking through real-world interactions on the ChatPulse application:

<div style="position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden; max-width: 100%; border-radius: 12px; box-shadow: 0 4px 20px rgba(0,0,0,0.15); margin: 25px 0;">
  <iframe 
    src="https://www.youtube.com/embed/br8FXBzj4Yk" 
    title="ChatPulse Application Video Demo" 
    style="position: absolute; top: 0; left: 0; width: 100%; height: 100%; border: 0;" 
    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" 
    allowfullscreen>
  </iframe>
</div>
