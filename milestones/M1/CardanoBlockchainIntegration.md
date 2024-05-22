# Cardano Blockchain Integration Architecture Overview

## Project Context: Tokenizing Agricultural Profits
Our project aims to revolutionize agricultural investments by tokenizing agricultural profits and providing transparent, verifiable returns to investors. By leveraging Cardano's blockchain capabilities, we ensure secure transactions, robust identity management, and efficient data retrieval, all crucial for the project's success.

![Project Overview](https://github.com/wseeds-sas/AgroTechnologyCardanoDocs/blob/docs/WD-565-initial-cardano-doc/milestones/M1/project-overview.png?raw=true)

## Cardano Blockchain Data Retrieval

### Blockfrost API Integration
**Purpose**: Facilitate direct blockchain data access without a dedicated node, offering scalable and efficient data retrieval crucial for tracking investment performance and agricultural output.

**Features**:
- **REST API**: Queries for transactions, addresses, and metrics.
- **Scalability and Security**: High availability and secure token-based access.

**Usage**:
- **Setup**: Register and configure API token within the application.
- **API Calls**: Fetch transaction histories, token balances, etc., to provide real-time updates to investors on their agricultural token holdings.
- **Data Processing**: Integrate data into the platform to display balances and transaction details, ensuring transparency and trust.

**Cons**: Cost implications post-free tier.

**Alternatives**:
- [Koios](https://www.koios.rest/pricing/Pricing.html)
- [Gomaestro](https://www.gomaestro.org/pricing)

**Long-term Strategy**:
For immediate deployment, we are utilizing Blockfrost for its speed and ease of setup. However, our long-term vision includes transitioning to an open-source solution like Ogmios or developing our own infrastructure. This approach aligns with our goal to eventually make the entire project open-source, providing greater control over data management and fostering community contributions.

### Open Source Option: Ogmios
Direct interaction with a local cardano-node via JSON+RPC-2.0, offering greater control over integration and deeper involvement in operational management.

**Cons**: Requires in-house node management.

**Future Considerations**:
While we are starting with a service like Blockfrost for rapid development, we aim to transition to an open-source infrastructure. This will involve managing our own node, ensuring all components of the project remain transparent and publicly accessible, promoting broader community engagement and contributions.

## Atala PRISM for Digital Identity Management

Atala PRISM ensures secure and verifiable identity management for all stakeholders involved—farmers, investors, and intermediaries—enhancing trust and transparency in the agricultural investment process.

**Components**:
- **Cloud Agent**: Manages decentralized identifiers (DIDs) and verifiable credentials (VCs) for participants.
- **Wallet SDKs**: Allow stakeholders to store credentials and respond to proof requests securely.
- **Mediator**: Facilitates secure message relay between Cloud Agents and Wallet SDKs, ensuring reliable communication.

### Usage in Project Context:
- **Agent Deployment**: Set up Cloud Agents via Docker; configure for issuer and verifier roles to handle identities of farmers and investors. This ensures that only verified participants can engage in token purchases and other critical interactions.
- **Wallet Interaction**: Implement Wallet SDKs to manage credentials, enabling investors to verify the authenticity of their agricultural token holdings. This is crucial for maintaining trust in the system, as illustrated in the project's process flow.
- **Mediation Setup**: Ensure continuous connectivity and secure message relay, crucial for maintaining trust and data integrity. This ensures that every step of the agricultural process, from planting to profit distribution, is securely recorded and verifiable.

### Integration with Project Flow:
1. **Token Holder (Step 1)**: Uses Atala PRISM for identity verification before purchasing tokens (AGRT).
2. **Investment (Step 2)**: Verified investors can buy tokens, which are then used to fund agricultural activities.
3. **Farmer (Step 3)**: Farmers, verified via Atala PRISM, utilize funds for cultivation, tracked via IoT sensors and AgroChat for real-time data.
4. **Traceability (Step 4)**: All farming activities, from planting to harvesting, are documented and verified through Atala PRISM, ensuring transparent and trustworthy processes.
5. **Harvest and NFTs (Step 4)**: Harvest information is recorded, and NFTs are generated, representing the yield and profitability of crops.
6. **Logistics and Consumer (Steps 5 & 6)**: Traceability ensures that logistics and final product quality are verifiable, building consumer trust.
7. **Profit Distribution (Step 7)**: Farm income and ROI distribution are managed and verified through the Atala PRISM infrastructure, ensuring that profits are fairly and transparently distributed to token holders.

**Benefits**:
- **Enhanced Security and Privacy**: Ensures that personal and financial data of investors and farmers are managed securely.
- **Interoperability**: Adheres to global standards, facilitating seamless integration with other systems and services.

## MeshJS Library Integration for Web3 Front-Ends
Enhance user experience by managing wallet interactions and other client-side operations directly from the browser, enabling investors and farmers to interact with the platform seamlessly.

**Features**:
- **Wallet Creation and Transaction Management**: Allow users to create and manage their wallets, facilitating transactions related to their agricultural token investments.
- **Security**: Robust measures to protect user data, ensuring that all interactions and transactions are secure.

**Usage**:
- **Library Setup**: Include MeshJS in the project, configured for interaction with Cardano's blockchain.
- **User Interface and Interaction**: Design intuitive interfaces for wallet management and transaction operations, making it easy for investors to track and manage their agricultural investments.

## Process Overview
1. **Token Purchase**: Investors purchase tokens representing specific farmland, enabling participation in agricultural activities.
2. **Investment in Cultivation**: Funds from token sales are reinvested in agricultural infrastructure, agronomic practices, and necessary logistics.
3. **Real-time Traceability**: Implement advanced technology for recording and documenting every step of the cultivation process, stored securely on the blockchain.
4. **Quality Certifications**: Generate real-time quality certificates, ensuring compliance with good agricultural practices and providing assurance to consumers.
5. **Data Analysis and Optimization**: Use AI and data analytics to optimize resource utilization, improve productivity, and make informed decisions.
6. **Harvest Certificates and Investor Transparency**: Generate NFTs for harvested crops, providing detailed information and transparency to investors about their investments.

## Conclusion
Integrating Blockfrost, MeshJS, and Atala PRISM within our Cardano-based platform streamlines the process of tokenizing agricultural profits and distributing them to investors. This architecture supports rapid development and ensures our application is secure, scalable, and user-friendly, paving the way for future enhancements and broader adoption.

By leveraging these technologies, we enhance transparency and trust, key components in attracting and retaining investors while providing farmers with the tools needed to participate in the digital economy.
