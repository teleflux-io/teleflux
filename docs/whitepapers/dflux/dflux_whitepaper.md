---
abstract: |
  Vertical IoT solution vendors relay on telecom operators (connectivity providers)
  and IoT platform operators (device and application management and message routing providers)
  in order to bring connected smart products to the market. High prices of IoT connectivity,
  low wireless coverage, and network unadapted for low-power battery-powered devices
  has been hindering IoT adaption for years. This coupled with high prices of running
  IoT platform in the cloud or depending on proprietary IoT cloud platform provider
  presents today a real blocker for high-volume IoT deployments. Additionally, as more and more
  stories of hacked IoT devices fill the news, IoT security is one of the top concerns.

  dFlux is globaly decentralized blockchain-based IoT system that provides high-coverage
  telecom connectivity, IoT platform and high security at very low cost.
---

# Introduction
dFlux is global and decentralized IoT telecommunication system and SW platform for enabling
IoT sensor and actuator connectivity.

It provides:

- Global LPWAN and other wireless coverage
- Billing system based on `ERC20` token
- IoT platfrom for device and application management
- Network security based on Ethereum blockchain with BFT consensus and immutability

Anyone will be able to participate in dFlux system - either as a vendor, operator, application developer or user.
Participants might come and leave at any time, while blockchain network assures security,
resistance to malicious-acting nodes and monetary incentivisation for network maintainers.

Since everybody can become a network maintainer with monetary compensation,
involvement of high number of nodes will enable ultra-low-cost long-range wireless
network installation and maintenance, while assuring wireless coverage
that would be unbeatable by the competition.

This will lower the overall price of service and enable low-cost, high-quality,
no-roaming (global) IoT network for next generation of IoT sensors and other devices.

# Stakeholders
We can identify following stakeholders of dFlux system:

- Solution (device and application) vendors
- Device owners (can be the same entities as solution vendors)
- Gateway operators
- IoT platform operators

## Solution (Device and Application) Vendors

IoT solution is based on smart-devices (usually battery powered wireless IoT sensors or actuators)
and an IoT application that controls these devices.

Solution vendors create IoT devices and pairing applications.

They relay on existing wireless network connectivity provided by gateway operators
and device and application management and messaging capabilities provided by IoT platform operators.

## Device Owners
Device owners are end-users of the IoT devices and applications. They are buying devices from solution vendors.

In some cases solution vendor and device owner can be the same entity.

## Gateway Operators
Gateway operators are key players in dFlux telecom system. They provide long-range low-power
low-cost wireless connectivity for IoT devices with very high geographical coverage.

Anyone can become a gateway operator by obtaining low-cost gateway hardware box. dFlux gateways
are made to be plug-and-play, so all that gateway operator has to do is to plug the box into the power.

Once installed at gateway operator premises, gateway provides long-range wireless connectivity that can
cover up to 30km perimeter. That means that only a few of these base-stations are sufficient to cover an average city area.

IoT devices connect to the nearest (best signal quality) gateway and communicate with the network.

Gateway operator is remunerated in FLX tokens in dependence of the traffic quantity that flows through the gateway.

## IoT Platform Operators
IoT platform operators are network nodes that run open-source Apache-2.0 licensed Mainflux[^mfx] IoT platform

Solution vendors search through the catalog of available IoT platform nodes in the dFlux system and choose the one
that they want to connect their application to.

IoT platform operators are remunerated in FLX tokens in dependence of IoT messages (traffic) they route
and number of applications and devices connected to them.


[^mfx]: Mainflux[@mfx] (<https://www.mainflux.com>) is modern, scalable, secure open source and patent-free IoT cloud platform written in Go. It accepts user, device, and application connections over various network protocols (i.e. HTTP, MQTT, WebSocket, CoAP), thus making a seamless bridge between them. It is used as the IoT middleware for building complex IoT solutions.

# System Architecture

dFlux is based on Ethereum blockchain-connected architectural blocks, wich together form full-blown telecom system.
This system is capable to provide wide-coverage long-range low-power wireless connectivity and complete management features, alongside
with billing and payment via Ethereum blockchain using `ERC20`-compatible `FLX` token.

Main architectural parts of the system are:

- End clients - IoT devices and applications
- Wireless gateways - i.e. base-stations
- System backend in the form of blockchain network nodes
- IoT platform based on Mainflux


\begin{figure}
\begin{center}
\begin{tikzpicture}[>=stealth]

  % Masernodes
  \node[draw, minimum width=2cm, minimum height=1cm, anchor=center, text width=2cm, align=center] (M2) {Mainflux\\2};
  \node[draw, minimum width=2cm, minimum height=1cm, below of=M2, text width=2cm, align=center, fill=gray!20] (E2) {ETH\\2};

  \node[draw, minimum width=2cm, minimum height=1cm, xshift=-3cm, yshift=1.5cm, above of=M2, text width=2cm, align=center] (M1) {Mainflux\\1};
  \node[draw, minimum width=2cm, minimum height=1cm, below of=M1, text width=2cm, align=center, fill=gray!20] (E1) {ETH\\1};

  \node[draw, minimum width=2cm, minimum height=1cm, xshift=3cm, yshift=1.5cm, above of=M2, text width=2cm, align=center] (MK) {Mainflux\\k};
  \node[draw, minimum width=2cm, minimum height=1cm, below of=MK, text width=2cm, align=center, fill=gray!20] (EK) {ETH\\k};

  % Gateways
  \node[draw, minimum width=1cm, minimum height=2cm, xshift=0cm, yshift=-6cm, below of=M1, text width=2cm, align=center, fill=gray!20] (GW1) {Gateway\\1};
  \node[draw, minimum width=1cm, minimum height=2cm, xshift=0cm, yshift=-6cm, below of=MK, text width=2cm, align=center, fill=gray!20] (GWM) {Gateway\\m};

  % Line
  \node[above of=GW1, xshift=-3cm, yshift=1.5cm] (A) {};
  \node[above of=GWM, xshift=3cm, yshift=1.5cm] (B) {};
  \draw[dashed] (A) -- (B);
  \node[above of=B, xshift=-1.7cm, yshift=-0.5cm] (BL) {Blockchain Network};
  \node[above of=GW1, xshift=0cm, yshift=1.5cm] (C) {};
  \node[above of=GWM, xshift=0cm, yshift=1.5cm] (D) {};

  % Devices
  \node[draw, minimum width=1cm, minimum height=1cm, xshift=-1.5cm, yshift=-2cm, below of=GW1, text width=1.5cm, align=center] (D11) {Device\\11};
  \node[draw, minimum width=1cm, minimum height=1cm, xshift=1.5cm, yshift=-2cm, below of=GW1, text width=1.5cm, align=center] (D1N) {Device\\1n};

  \node[draw, minimum width=1cm, minimum height=1cm, xshift=-1.5cm, yshift=-2cm, below of=GWM, text width=1.5cm, align=center] (DM1) {Device\\m1};
  \node[draw, minimum width=1cm, minimum height=1cm, xshift=1.5cm, yshift=-2cm, below of=GWM, text width=1.5cm, align=center] (DMP) {Device\\mp};

  % Applications
  \node[draw, minimum width=2cm, minimum height=1cm, xshift=-1.5cm, yshift=2cm, above of=M1, text width=1cm, align=center] (APP11) {App\\11};
  \node[draw, minimum width=2cm, minimum height=1cm, xshift=1.5cm, yshift=2cm, above of=M1, text width=1cm, align=center] (APP1J) {App\\1j};

  \node[draw, minimum width=2cm, minimum height=1cm, xshift=-1.5cm, yshift=2cm, above of=MK, text width=1cm, align=center] (APPK1) {App\\k1};
  \node[draw, minimum width=2cm, minimum height=1cm, xshift=1.5cm, yshift=2cm, above of=MK, text width=1cm, align=center] (APPKZ) {App\\kz};

  % draw the paths and and print some Text below/above the graph
  \path (E1) edge[bend right=40] (E2);
  \path (E1) edge[-] (EK);
  \path (E2) edge[bend right=40] (EK);

  \path (C) edge[<->] (GW1);
  \path (D) edge[<->] (GWM);

  \path (D11) edge[-] (GW1);
  \path (D1N) edge[-] (GW1);
  \path (DM1) edge[-] (GWM);
  \path (DMP) edge[-] (GWM);
  \path (M1) edge[-] (APP11);
  \path (M1) edge[-] (APP1J);
  \path (MK) edge[-] (APPK1);
  \path (MK) edge[-] (APPKZ);
\end{tikzpicture}
\end{center}
\caption{dFlux System Architecture}
\label{fig:arch}
\end{figure}

## End Clients (Devices and Applications)
System end clients are IoT devices and applications.

### Devices
Devices are smart connected devices, very often constrained and battery powered.
That means that IoT wireless connectivity must be of type LPWAN (Low-Power Wide-Area Network). Additionally, for lower ranges devices might come
with BLE (Bluetooth Low Energy) and Wi-Fi connectivity.

Devices are connected to gateways and communicate via LoRaWAN (in case of LoRa network) or some other application protocol supported by Mainflux IoT platform:
MQTT, CoAP, WebSocket or HTTP REST.

### Applications
IoT applications are made by solution vendors and are usually the applications that communicate with devices via IoT platform middleware.
Applications use some of the usual IoT protocols - like HTTP, WebSocket, MQTT or CoAP - and relay on IoT platform APIs for communication
and asynchronous event delivery.

Applications communicate directly with Mainflux IoT platform that runs on every dFlux Masternode within blockchain network.

## Gateways
Gateways are network base-stations, operated by gateway owners in return for FLX tokens. These base-stations provide wireless coverage and connectivity to devices.

Gateways support several types of wireless networks:

- **LoRaWAN** - for long-range low-power wireless connectivity
- **BLE** - Bluetooth Low Energy became one of the essential IoT wireless protocols for connecting low-to-mid range devices
- **WiFi** - certain devices can tolerate and demand WiFi connectivity

Gateways are connected to Ethereum public blockchain network as a light nodes[^lnd]. As a consequence, they are capable to regularly pull
the configuration parameters and security updates, and securely communicate with blockchain Masternodes.

[^lnd]: The purpose of the light client protocol is to allow users in low-capacity environments (embedded smart property environments, smartphones, browser extensions, some desktops, etc) to maintain a high-security assurance about the current state of some particular part of the Ethereum state or verify the execution of a transaction. - [https://github.com/ethereum/wiki/wiki/Light-client-protocol](https://github.com/ethereum/wiki/wiki/Light-client-protocol). Additionally, some instructions
for running Etehreum light clients on RPi-type embedded computers can be found here: [https://github.com/ethereum/wiki/wiki/Raspberry-Pi-instructions](https://github.com/ethereum/wiki/wiki/Raspberry-Pi-instructions)

## Masternodes
Masternodes are full Ethereum nodes that maintain and validate transactions and enable secure p2p messaging via Ethereum `Swarm PSS` protocol[^pss] and/or `Whisper`[^wsp].
Each Masternode runs a set of Ethereum Smart Contracts and a Mainflux IoT platform in the form of Ethereum dApp.

[^pss]: `PSS` enables message relay over swarm. This means nodes can send messages to each other without being directly connected with each other, while taking advantage of the efficient routing algorithms that swarm uses for transporting and storing data. - [https://github.com/ethersphere/go-ethereum/tree/swarm-network-rewrite/swarm/pss](https://github.com/ethersphere/go-ethereum/tree/swarm-network-rewrite/swarm/pss)

[^wsp]: In a nutshell whisper is a communication protocol for DApps to communicate with each other. - [https://github.com/ethereum/wiki/wiki/Whisper](https://github.com/ethereum/wiki/wiki/Whisper)

## IoT Platform
dFlux uses Mainflux IoT platform, industrial open-source Apache-2.0 licensed IoT platform that enables device and application management and
secure IoT messaging via multi-protocol broker, supporting MQTT, CoAP, WS and HTTP application protocols.

Mainflux IoT platform runs on the top of each Masternode as an Ethereum dApp, and is capable to share configuration and device-provisioning
information with other blockchain nodes - notably with Gateways.

Beacuse IoT platform runs as a dApp, it gets all the service payment information from underlying blockchain.

IoT platform is run and maintained by platform operators who base their business on providing IoT platform SaaS and charge
solution vendors for connecting their applications and devices to the platform. SaaS services are charged in FLX tokens.

# Mode of Operation
The goal of dFlux telecom system is to enable bidirectional communication between IoT devices and applications, i.e. to enable
uplink (from devices to network) and downlink (from network to connected devices) data traffic.

Central role in wireless connectivity layer is played by gateways, which act as network base-stations. They accept connections and
data packets from end devices and transfer them towards IoT platform, which further routes them to connected applications.

Each gateway runs an Ethereum light node client, which is adopted for running on small embedded devices. Because
each gateway is connected to Ethereum blockchain network via light client, it can download the necessary configuration and
security updates from the network.

_Modus operandi_ is following:

- Upon initial set-up, each gateway announces itself to the network by calling a pre-defined Smart Contract.
To mitigate various security issues and assure QoS, only certified gateways are accepted on the network.
dFlux Foundation assures and issues gateway certifications and sets-up gateway onboarding Smart Contract in Ethereum network.

- As a result of successful onboarding Smart Contract invocation,
a gateway ID is published (broadcasted) to all dFlux Masternodes via
Ethereum `Whisper` or Ethereum `Swarm PSS` messaging protocols

- Upon reception of this message, each Masternode:
    1) Provisions gateway digital twin in it's Mainflux IoT dApp and
    2) Sends back a private response message to gateway with:
        a) ID of the Mainflux IoT platform running on this Masternode and
        b) Access credentials for just provisioned gateway digital twin on Mainflux running Masternode

- Each gateway stores locally mapping `<mainflux_dapp_id>:<masternode_addr>` and mapping `<mainflux_dapp_id>:<gw_mainflux_credentials>`

- Because gateway now disposes all necessary credentials for each Mainflux dApp, it can attach directly to them
via long-lasting bi-directional MQTTS (TLSv1.3 encoded MQTT) connection (usually with `QoS=1` to protect from intermittent disconnections)

- Upon every initial connection of new Mainflux dApp (i.e. addition of new Masternode to blockchain network), an onboarding Smart Contract
is invoked and:
    1) New `mainflux_dapp_id` is broadcasted to all gateways in the system and
    2) List of all `gateway_id` is sent to new Masternode's Mainflux dApp, so it can provision digital twins for each of them and issue
    them the access credentials (via private message, as explained before)

Devices belong to solution vendor, who pre-provisions each device in Mainflux IoT platform on one of the Masternodes
(each Mainflux IoT platform has a unique `mainflux_dapp_id`). Solution vendor collects necessary data from
Mainflux dApp during provisioning phase, like `device_id`, `mainflux_dapp_id` - ID of Mainflux dApp instance
for which device was provisioned, and similar.

One of the most important information obtained form this Mainflux dApp instance during provisioning phase
are the credentials and certifications to authenticate given device to this device and encrypt it's data traffic
so it can be decrypted and understood only by this Mainflux dApp instance.

This way data can flow from device through various gateways and routers, but will stay completely obscure for them.

## Uplink

- Device is pre-programmed (via internal firmware) to send send an encrypted `CONNECT` message with
unencrypted message header with `mainflux_dapp_id` upon connection to the gateway.

- Gateway reads this header and finds `gw_mainflux_credentials` and `masternode_addr` from local database, then forwards the message with device's ID in the header to the Masternode's
IoT platform via Mainflux public API.

- Mainflux decrypts the message and determines if the device holds necessary credentials (each message is cryptographically signed by the device).
    - If yes, Mainflux stores `<device_id>:<gateway_id>` mapping in local storage and replies to the gateway either `OK` - on which gateway accepts the connection from device
    - If not, Mainflux ignores the connection and replies `NOK`, on which gateway refuses the connection and blacklists the device.

- Additionally, if the device connection is accepted, Mainflux dApp stores `<device_id>:<qos>` mapping, where following the MQTT analogy
 `QoS=0` means "at most once" and `QoS=1` means "at least once" message delivery. I.e. QoS informs the Mainflux dApp if the system
 if the message should be retained for a given device.

- If connection is accepted, gateway routes all messages to designated Mainflux IoT instance following the aforementioned routing scheme.

- Both gateway and Mainflux IoT dApp keep a track of routed traffic.

- Gateway remuneration can be solved in two ways:
    1) Mainflux IoT dApp periodically pays gateway for it's services in FLX tokens.vIf gateway finds that payment is lacking and/or is inadequate,
it can blacklist the Mainflux IoT dApp - which will in that case be punished, loosing the connectivity to all it's devices in this area.
    2) By opening a real-time uRaiden[^urd] micro-payment channel, where Mainflux IoT dApp will pay instantly for each message coming from the gateway

[^urd]: µRaiden (https://raiden.network/micro.html) is a payment channel framework for frequent, fast and free ERC20 token based micropayments between two parties.

## Downlink
- Application pushes a message to Mainlfux IoT dApp addressed to a particular device
- Mainflux dApp looks up in it's `<device_id>:<gateway_id>` and  `<device_id>:<qos>` mappings and pushes this info alongside
with the message to the appropriate gateway.

> N.B. _If `<device_id>:<gateway_id>` mapping does not exist, that means that device was not yet onboarded into the network. The message would be simply
dropped by the Mainflux dApp informing the application about the failure._

- Gateway receives the message and if the device is connected - it pushes the message straight away to the device.
If the device is currently in the sleep mode and unavailable for communication, gateway looks at the QoS mode:
    - If the `QoS=0`, gateway  drops the message
    - If the `QoS=1`, gateway retains the message in the local storage, to be sent upon device connection is re-established

- Getaway monetary remuneration in FLX tokens is the same as in case of uplink messaging

# Gateway Hardware
Gateways play a central role in dFlux system and greatly contribute to main innovation behind dFlux - _Uberization_ of IoT telecom network connectivity.
This inherently brings several challenges, because of contradictory requirements:

- In order for this _Uberization_ to be feasible, gateway hardware must be available at low-cost, so it can be produced and delivered to gateway operators in mass
- In order to assure high connectivity QoS, network hardware must be of the good quality

Additionally, to assure high security standards, gateway hardware must be physically and cryptographically protected from anti-tampering,
as it will be explained subsequent chapter related to security threats.

With advancement of embedded computers it becomes feasible to construct a gateway with inexpensive high-quality and highly-secure
Linux embedded system with all necessary WiFi, BLE and LoRaWAN connectivity.
8-channel LoRaWAN modems based on Semtech's `SX1301` SoC can be found on the market for sub-$100, and whole gateway cost can be estimated to be in the range of $100-200.
This opens the door for mass production and supply of dFlux gateway hardware, which can be leased or sold to the gateway operators.

Gateway boxes are small, easy to install and are build to be plug-and-play: gateway owner just plugs the gateway box into the electricity outlet
and starts providing the network connectivity in the installation area (15-30km perimeter) and earning FLX tokens.

Through the program of Gateway Certification, established by dFlux Foundation, system assures physical and cryptographic anti-tampering mechanisms
necessary for security regulations.

# FLX Token
FLX token is utility token of dFlux system. It is used to assure fair and secure functioning of the system, as well as to enable token economy within the system.

Primary purpose of the token will be to fuel the system - it will be used to tokenize the value of digital assets (i.e. IoT connectivity and IoT cloud platform services) and facilitate their exchange.

IoT platform providers will use FLX token as a representation of value of their IoT platform SaaS services in the form of APIs. Gateway operaors will use FLX token to represent the value of their IoT connectivity enablers. Solution vendors will buy IoT platform services and wireless connectivity in FLX token. Device owners will pay device subscription plans in FLX tokens.


# Security Threats
Every communication system brings security and privacy challenges. Traditional telecom network operators protect from the
attacks in various ways, most of which are inapplicable in the decentralized and publicly-opened system like dFlux.

This chapter explains how dFlux system mitigates identified security threats.

## Gateway Anti-Tampering
One of the biggest security threats of dFlux system is that the network base-stations (i.e. gateways) are at the reach of various individuals,
as they are installed and maintained by gateway operators on their own premises.

Traditional telecom network installations protect physical access to base-stations by enclosing them in designated protected
telecom sites that belong to the operator who owns the equipment.

dFlux mitigates this security threat by implying following approaches:

- All traffic that flows through the gateway is encrypted, and gateway only routes the traffic without possibility to decrypt and understand communication.
Traffic is decrypted only at it's final destination - i.e. in the Mainflux dApp instance or at the end device.

- All gateways are physically sealed and protected by anti-tampering sensors which automatically self-destroy chip fuses upon tampering detection

- Additionally, all access to the embedded electronics is prevented - UART and JTAG are disabled and all SoCs are sealed with epoxy, preventing the probing access

- Every SW image running on gateway is cryptographically signed and various security protection methods are applied - like running SW audit daemons and FIM agents
that compare file and process fingerprints with blockchain anchored hashes

On every detected tampering attempt, a warning is broadcasted via blockchain network to all Masternodes, which automatically blacklist this gateway.

## X.509 Certificates, PKI and AES
All traffic in dFlux system is encrypted:

- Traffic on Ethereum blockchain network is seemlesly encrypted by design
- Traffic between Mainflux dApp instances and gateways is TLSv1.3 encrypted (in the form of MQTTS, for example)
- Traffic between end devices and gateways is encrypted in dependance of physical protocol: WiFi uses WPA2, BLE and LoRaWAN realy on AES

There is however one particularity of dFlux system in comparison of traditional telecom systems: gateways (network base-stations) do not belong to the network operator.
Actually, there is no network operator in decentralized system by design - network is auto-operated by Smart Contracts on the blockchain and Masternode dApps.
This is why the rule _DO NOT TRUST ANYONE_ must be strictly applied in these kind of systems.

Mainflux dApp instances do not trust gateways and must hide all traffic that is routed through the gateways by encrypting it with encryption keys
only known to interested parties - end devices that are provisioned in this Mainflux dApp instance.

Because of this, devices can not use traditional JWT or similar bearer token authentication schemes (in order to be delivered to end destination,
Mainflux dApp instance, bearer token would have to go through gateway which can sniff and discover the token).

To prevent this from happening, Mainflux dApp issues client-side certificates (in the case when PKI encryption is used) or AES keys
(in the case when symmetric encryption is used) to be burned directly in device's firmware.

Devices use these keys known only to them to encrypt all messages.

Gateways are incapable of decrypting the messages and can only route the traffic to appropriate Mainflux dApp instance, which knows how to decrypt them.

## Replay Attack
Wireless messages transfered over the air interface can suffer of so called _Replay attack_[^rpl]. An attacker can sniff _over-the-air_ traffic
by tuning on the same radio frequency (using SDR equipment for example), and later use the same messages to spoof the network.

Even though the messages are encrypted and completely incomprehensible for the attacker, they contain all the necessary signatures
(signed previously by the device during the message forming phase) needed for messages to be authenticated by the network as they look
completely valid to the receiver (in this case Mainflux dApp).

In order to protect from replay attacks, dFlux messaging protocol imposes `message_id` stamping of every message (timestamps can equally be used).

Destination Mainflux dApp service takes a track of received messages, and drops all duplicated messages. Additionally, upon detection of replay attack attempt
detection it can inform the gateway to blacklist the attacker.  

[^rpl]: A replay attack (also known as playback attack) is a form of network attack in which a valid data transmission is maliciously or fraudulently repeated or delayed. This is carried out either by the originator or by an adversary who intercepts the data and re-transmits it, possibly as part of a masquerade attack by IP packet substitution. This is one of the lower tier versions of a "Man in the middle attack." - [https://en.wikipedia.org/wiki/Replay_attack](https://en.wikipedia.org/wiki/Replay_attack)

# dFlux Foundation
dFlux Foundation, a non-for-profit association, will be formed to maintain and regulate system architecture, QoS and proper functionality.

Main role of dFlux Foundation is to lead the dFlux Gateway Certification Program, i.e. to issue and stamp proper certificates for accredited Gateway manufacturers.
Gateway Certification Program guarantees that only certified gateways will be appear on the network. It also assures new gateway provisioning and onboarding by defining
an Ethereum Smart Contract related to this `gateway_id`.

dFlux Foundation Committee membership is publicly open to all holders of over 10k FLX tokens.

# Conclusion
Based on many reports[^arm], we can be sure of one thing: there is gold in the mountains of data. A way is needed to mine all this gold - a platform is needed to monetize all this data. dFlux is a an enabler that will unlock this huge potential.

dFlux builds global decentralized IoT telecom system based on blockchain, that is secure and scalable. It enables new token economy - FLX token will be used as an utility token of dFlux system, and will be used to enable fair and secure functioning of the system as well to enable billing facilities.

[^arm]: In the paper 'Route to trillion devices', ARM predicts one trillion IoT devices by 2035 with $5 trillion in market value [@arm].

# References
