---
abstract: |
  Edge computing allows data produced by Internet of Things (IoT) devices to be processed closer
  to where it is created instead of sending it across long routes to data centers or clouds.
  This reduces the communications bandwidth needed between sensors and the central datacenter
  by performing analytics and knowledge generation at or near the source of the data.

  Although there is high need to obtain the insights from the network edge, until recently there was
  not an easy way to achieve this goal because of several reasons:
  installation and maintenance of edge gateways in not trivial and is costly,
  there is no standardized edge system software platform for which applications
  can be made, there is no easy way to provide remote access to edge equipment to 3rd parties
  in a secure manner, and similar.

  Thanks to the recent advancements in edge platform standardization led by Linux Foundation's EdgeX Foundry project
  and possibilities open by a public blockchains, there is an opportunity to construct easy-to-access and
  and easy-to-use global edge computing platform that would be economically feasible and create new value.

  dEdge is global and decentralized edge computing platform and microservice marketplace for enabling
  monetization of geographically-dispersed network edge HW equipment access and
  specialized system application development and deployment.
---

# Introduction
dEdge is global and decentralized edge computing platform and microservice marketplace for enabling
monetization of geographically-dispersed network edge HW access and specialized system application development.

It provides:

- Access to edge computing capacity of the network edge gateways
- Access to sensors, actuators and other HW peripherlals attached to these gateways
- Deployment of custom SW on the network edge
- Payment system based on `ERC20` token
- Network security based on Ethereum blockchain with BFT consensus and immutability

dEdge relays on EdgeX Foundry platform, which is a vendor-neutral, open-source, Apache-2.0 licensed project under the umbrella of Linux Foundation.
EdgeX Foundry is building a common open framework for IoT edge computing. At the heart of the project is an interoperability
framework hosted within a full hardware- and OS-agnostic reference software platform to enable an ecosystem of
plug-and-play components that unifies the marketplace and accelerates the deployment of IoT solutions.

EdgeX Foundry proposes a loosely-coupled tiered IoT architecture by allowing customers to deploy a mix of plug–and–play microservices
on compute nodes at the edge depending on the capability of the host devices, where they sit in the solution stack, and the use case.

Because of these standardization characteristics of an underlying EdgeX platform, it becomes possible to deploy a custom microservice on
any EdegeX-compliant gateway - as long as this microservice respects the EdgeX API standard.

dEdge decentralized platform forms a marketplace on Ethereum blockchain on which EdgeX-compliant gateways advertise their computing resources
and sell them to users who deploy their custom EdgeX-compliant microservices for a monetary compensation in `ERC-20`-compliant `EDG` token.

# Stakeholders
We can identify following stakeholders of dEdge system:

- Edge gateway (HW) operators
- Edge computing platform buyers

## Edge Gateway Operators

Edge gateway operators install and maintain EdgeX Foundry-compliant gateways.

A set of sensors and actuators can be attached to these gateways, and edge gateway operators are interested in selling
the access to these gateway computing platforms (and consequently access to attached sensors and actuators) to
interested parties in exchange for EDG tokens.

## Edge Computing Platform Buyers

Edge computing platform buyers are interested to gain insights on the network edge. Potentially they can do this
by using IoT data marketplace like Monetasa.

However, main problem in buying this pre-selected data from the offered catalog is that:

- Data on the edge is often perishable, with short-lasting value (data is valuable just a few seconds after it's collection)
- Collected data amount can be huge, so data must be processed directly on the edge in order for this processing to be economically justifiable
- Response on certain edge events must be instant - there is no time to send data to the cloud and process it there, then send responses back to the edge

Moreover, process of collecting data from the sensors and process of driving the actuators can be custom and application specific, and thus must be defined
by a party who creates the application, not by an edge gateway operator (who can not predict all the ways in which data should be collected and sent to Monetasa).

All of this demands direct access to edge gateway computing hardware, on which  platform buyer can run it's own application SW for a leased period of time
and in a secured, sandboxed manner.

# System Architecture
dEdge system is based on Ethereum blockchain and IPFS decentralized file system.

Ethereum blockchain is used for several purposes:

- Discovery
- Payment
- Smart Contracts

IPFS file system is used for transfer of microservices in form of Docker images.

_**Seller**_ is an EdgeX-compliant edge gateway that sells it's computing resources.

_**Buyer**_ is an entity interested in buying edge computing resources, and it prepares and sends Docker image to be executed on the _**Seller**_'s gateway.

\begin{figure}
\begin{center}
\begin{tikzpicture}[>=stealth]

  % Blockchain
  \node[draw, minimum width=4cm, minimum height=2cm, anchor=center, text width=8cm, align=center, fill=gray!20] (BC) {Ethereum\\Blockchain};

  % Seller
  \node[draw, minimum width=2cm, minimum height=2cm, xshift=-3cm, yshift=3cm, above of=BC, text width=2cm, align=center, fill=gray!20] (S) {Seller};

  % Buyer
  \node[draw, minimum width=2cm, minimum height=2cm, xshift=3cm, yshift=3cm, above of=BC, text width=2cm, align=center, fill=gray!20] (B) {Buyer};

  % IPFS
  \node[draw, minimum width=4cm, minimum height=2cm, anchor=center, xshift=0cm, yshift=7cm, above of=BC, text width=8cm, align=center, fill=gray!20] (I) {IPFS};

  % draw the paths and and print some Text below/above the graph
  \path (S) edge[-] (BC);
  \path (B) edge[-] (BC);

  \path (S) edge[-] (I);
  \path (B) edge[-] (I);

  \path (S) edge[<->] (B);

\end{tikzpicture}
\end{center}
\caption{dEdge System Architecture}
\label{fig:arch}
\end{figure}

# Mode of Operation
The goal of dEdge platform is to enable a communication method and services via which Sellers can advertise their edge computing resources
and via which Buyers can discover advertised edge gateways. Additionally, dEdge enables a platform for deploying Docker images on Seller's gateways
and defines set of rules (protocol based on Ethereum Smart Contracts) for their communication and monetary settlement in EDG tokens.

_Modus operandi_ is following:

- Sellers advertise their capabilities by invoking `dedge_advertise` Smart Contract. Invocation of this contract is charged by the dEdge platform
buy several EDG tokens in order to prevent network spam, and also in return for platform services.

- Buyers polls for advertised announces, and select platform that fits their purposes.

- Buyer contacts selected Seller with an offer, and writes the hash of this offer into the blockchain

- If the Seller accepts the offer, it writes the offer's hash into the blockchain and invokes a Smart Contract which puts Seller and Buyer _in contract_

- For contract to be valid, Buyer must also deposit as an escrow an amount that will be payed to dEdge platform for its services
by calling `dedge_fee` Smart Contract

- From this moment on, Buyer and Seller can continue to communicated directly, via p2p messaging: for example via Whisper or Swarm PSS

- Buyer deposits some amount into uRaiden payment channel as a escrow and sends this proof to Seller

- If the seller accepts the proof, then Buyer prepares and sends the Docker image to Seller via IPFS

- Buyer's program is executed in Docker container on Sellers platform, and this program can communicate directly p2p with Buyer's backend applications

- Buyer regularly pays to Seller some EDG tokens via uRiden payment channel in the form of micropayments in order for deployed microservice to keep running

- Once program is terminated, both Buyer and Seller invoke `termination` Smart Contract, which produces the invoice

- `termination` Smart Contract in consequence invokes `dedge_fee` Smart Contract which collects the escrow fee from the Buyer

# EDG Token
EDG token is utility token of dEdge system. It is used to assure fair and secure functioning of the system, as well as to enable token economy within the system.

Primary purpose of the token will be to fuel the system - it will be used to tokenize the value of digital assets (i.e. edge computing capacity and resources
of edge gateway operators and microservices for microservice providers) and facilitate their exchange.

# Future Work
In addition to exiting platform services of trading with edge computing resources,
dEdge can be extended in the future to add an EdgeX Foundry application (micoservice) marketplace, based on Ethereum blockchain and EDG token.
This way dEdge would provide a catalog of specialized system and application SW that can be purchased by various parties to be run on the edge.

On this app marketplace we can identify two types of stakeholders:
- Micorservice (SW) vendors
- Microservice buyers

## Microservice Vendors
dEdge system enable a global platform of running custom SW on other people's edge gateways. This opens up an opportunity for
specialized SW development - companies and individuals might be interested in developing specialized microservices to be ready for deployment
on EdgeX Foundry-compliant gateways and sell them for EDG tokens.

## Microservice Buyers
Edge computing platform buyers would often be interested to buy ready-made set of SW components (microservices)
that can be run on edge gateway HW and produce desired results. This option can suit them better than writing their
own SW and speed up their time to market.

Additionally, edge gateway operators might be interested to buy ready-made SW components
to run them on their gateways and produce edge insights that they can
sell on dEdge platform.

# Conclusion
Based on many reports[^arm], we can be sure of one thing: there is gold in the mountains of data. A way is needed to mine all this gold - a platform is needed to monetize all this data. dEdge is a an enabler that will unlock this huge potential.

dEdge builds global decentralized IoT telecom system based on blockchain, that is secure and scalable. It enables new token economy - FLX token will be used as an utility token of dFlux system, and will be used to enable fair and secure functioning of the system as well to enable billing facilities.

[^arm]: In the paper 'Route to trillion devices', ARM predicts one trillion IoT devices by 2035 with $5 trillion in market value [@arm].

# References
