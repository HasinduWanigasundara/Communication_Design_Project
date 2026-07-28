# Two-Way Digital Paging System Using Software Defined Radios

<p align="center">
  <!-- Note: Place an isolated, transparent image of the BladeRF SDR in your Images folder and link it below -->
  <img src="Images/bladerf_transparent.png" alt="BladeRF SDR" width="400"/>
</p>

## 📌 Project Overview
This project transforms a standard software-defined radio (SDR) setup into a secure, reliable, packet-switched paging system capable of guaranteeing message delivery in noisy environments. Developed for the EN2130 Communication Design Project at the Department of Electronic and Telecommunication Engineering, University of Moratuwa, this system facilitates two-way text messaging with custom priority scheduling, AES encryption, and reliability protocols.

**Team NETLINK:**
*   Aroshana H.A.P (230058N)
*   De Mel D.J. (230121D)
*   Ratheeshan A.R. (230539P)[cite: 6]
*   Wanigasundara W.M.H. (230680M)[cite: 6]

---

## ⚙️ System Architecture

The core data flow relies on a custom Automatic Repeat Request (ARQ) protocol and strict priority scheduling. Below is the system architecture routing the signals from the Python GUI through the GNU Radio modulation pipeline[cite: 6]:

```mermaid
graph TD
    %% Python to TX Pipeline
    GUI_TX[GUI Window] --> MSG_Storage[MSG Storage]
    MSG_Storage --> MUX[MSG and ACK Mux]
    ACK_Gen[ACK Generator] --> MUX
    MUX --> Mod[Modulation]
    Mod --> TX[Transmit]

    %% RX to Python Pipeline
    RX[Receive] --> Demod[Demodulation]
    Demod --> Filter[MSG / ACK Filter]
    
    %% Filter Logic
    Filter -- ACK --> Recv_ACK[Received ACK]
    Recv_ACK --> MSG_Storage
    
    Filter -- MSG --> Seq_Check[Sequence Checker]
    Seq_Check --> GUI_RX[GUI Window]
    Seq_Check --> ACK_Gen
