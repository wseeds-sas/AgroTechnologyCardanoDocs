# Cardano Blockchain Integration Architecture Overview

## Cardano Blockchain Data Retrieval

### Blockfrost API Integration
**Purpose**: To facilitate data retrieval from the Cardano blockchain without the need to maintain a dedicated node. This service provides a scalable and efficient method to access blockchain data directly.

**Features**:
- **REST API**: An easy-to-use RESTful API that allows developers to query transactions, addresses, blocks, and various blockchain metrics.
- **Scalability**: Handles requests at scale, offering high availability and consistent performance, crucial for production environments.
- **Security**: Provides secure API access with authentication tokens, ensuring data integrity and preventing unauthorized access.

**Usage**:
- **Setup**: Register on Blockfrost, obtain an API token, and configure it within your application.
- **API Calls**: Use the API to fetch necessary blockchain data, such as transaction histories or token balances.
- **Data Processing**: Integrate fetched data into your application logic, such as displaying balances or processing transactions.

**Cons**: As a SaaS, Blockfrost offers a free tier, but it incurs costs after significant usage.

**Similar Options**:
- [Koios](https://www.koios.rest/pricing/Pricing.html)
- [Gomaestro](https://www.gomaestro.org/pricing)

#### Pricing:
![Blockfrost](https://github.com/wseeds-sas/AgroTechnologyCardanoDocs/blob/docs/WD-565-initial-cardano-doc/milestones/M1/blockfrost-pricing.png?raw=true)
![Koios](https://github.com/wseeds-sas/AgroTechnologyCardanoDocs/blob/docs/WD-565-initial-cardano-doc/milestones/M1/koios-pricing.png?raw=true)
![Gomaestro](https://github.com//wseeds-sas/AgroTechnologyCardanoDocs/blob/docs/WD-565-initial-cardano-doc/milestones/M1/gomaestro-pricing.png?raw=true)

### Open Source Option: Ogmios
Ogmios provides an HTTP/WebSocket API for interacting with a local cardano-node via JSON+RPC-2.0, offering higher control over integration and deeper involvement in operational management.

**Cons**: Requires managing node infrastructure in-house, which can be costly.

## MeshJS Library Integration for Web3 Front-Ends
**Purpose**: To manage wallet interactions and other client-side operations directly from the user's browser, enhancing the user experience by providing seamless interaction with the Cardano blockchain.

**Features**:
- **Wallet Creation**: Enables users to create and manage their own wallets within the application interface.
- **Transaction Management**: Facilitates the creation, signing, and submission of transactions without needing extensive blockchain knowledge from the users.
- **Security**: Implements robust security measures to protect user data and credentials, crucial for maintaining trust and integrity.
- **Open Source**: Open-source libraries provide transparency, community support, and continuous improvements, which are beneficial for security and feature enhancements.
- **Compatibility with React and Typescript**: Ensures that developers can use contemporary web development frameworks and languages to enhance application robustness and maintainability.

**Usage**:
- **Library Setup**: Include the MeshJS library in your project. Configure it to interact with Cardano's blockchain.
- **User Interface**: Design and develop intuitive interfaces for wallet management and transaction operations.
- **Interaction Handling**: Use MeshJS functions to handle blockchain interactions, such as sending ADA or custom tokens, within the application.

## Architectural Overview Diagram
The diagram visually represents how these components interact within the SDK architecture:
- External APIs (like Blockfrost) shown as the data retrieval layer.
- Front-end Libraries (like MeshJS) illustrated as the interface layer handling user interactions.
- Cardano Blockchain as the foundational layer providing the underlying blockchain functionality.

## Conclusion
Integrating Blockfrost and MeshJS simplifies the complexity of blockchain interactions and enhances the scalability of applications built on the Cardano platform. As part of the AgroTechnology Cardano project [fund 11](https://projectcatalyst.io/funds/11/cardano-use-cases-concept/agrotechnology-cardano), this path enables a faster development process, compatible with the testnet integration that will result from this project. Future exploration of multiple data retrieval systems (e.g., Koios, Gomaestro) should be within scope to avoid dependency on third-party services. This integration approach not only aligns with modern development practices but also ensures that your application is robust, scalable, and user-friendly.
