# Two-Way Digital Paging System Using Software Defined Radios

<p align="center">
  <!-- Note: Place an isolated, transparent image of the BladeRF SDR in your Images folder and link it below -->
  <img src="Images/bladerf_transparent.png" alt="BladeRF SDR" width="400"/>
</p>

## 📌 Project Overview
This project transforms a standard software-defined radio (SDR) setup into a secure, reliable, packet-switched paging system capable of guaranteeing message delivery in noisy environments[cite: 6]. Developed for the EN2130 Communication Design Project at the Department of Electronic and Telecommunication Engineering, University of Moratuwa[cite: 1, 6], this system facilitates two-way text messaging with custom priority scheduling, AES encryption, and reliability protocols[cite: 6].

**Team NETLINK:**
*   Aroshana H.A.P (230058N)[cite: 6]
*   De Mel D.J. (230121D)[cite: 6]
*   Ratheeshan A.R. (230539P)[cite: 6]
*   Wanigasundara W.M.H. (230680M)[cite: 6]

---

## ⚙️ System Architecture

The core data flow relies on a custom Automatic Repeat Request (ARQ) protocol and strict priority scheduling[cite: 6]. The system architecture routes signals between the Python GUI and the GNU Radio modulation pipeline through the following stages[cite: 6]:

*   **Transmission Pipeline:** Messages originating from the GUI Window are passed to the MSG Storage block[cite: 6]. The MSG and ACK Mux then combines data from the MSG Storage and the ACK Generator before passing it to Modulation and finally to the Transmit stage[cite: 6].
*   **Reception Pipeline:** Incoming signals are Received and passed through Demodulation before reaching the MSG / ACK Filter[cite: 6].
*   **Filter Logic:**
    *   **Acknowledgments:** Recognized ACKs are routed to the Received ACK block, which then updates the MSG Storage to clear the waiting buffer[cite: 6].
    *   **Messages:** Recognized Messages are routed to the Sequence Checker, which passes the validated data to the receiving GUI Window and triggers the ACK Generator to respond to the sender[cite: 6].
