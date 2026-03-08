# BlockChainHereICome
Entirely Blockchain.
```mermaid
graph TD
    %% --- Theme & Styles ---
    classDef core fill:#003566,stroke:#ffc300,color:#fff,stroke-width:3px;
    classDef layer fill:#1d3557,stroke:#457b9d,color:#fff,stroke-width:1px;
    classDef component fill:#2a9d8f,stroke:#264653,color:#fff,stroke-width:1px;
    classDef vuln fill:#6a040f,stroke:#d00000,color:#fff,stroke-width:2px;
    classDef flow fill:#fff,stroke:#000,color:#000,font-style:italic;

    %% --- Central Hub ---
    ROOT((<b>VOLUME 1:<br/>Protocol Fundamentals</b>)):::core

    %% --- BRANCH 1: The Node Infrastructure (Physical/Logic) ---
    ROOT --- INFRA[<b>I. Node Anatomy</b>]:::layer
    INFRA --> N_TYPES(Node Classifications):::component
    N_TYPES --> FN[Full Node: Validates all rules]
    N_TYPES --> LN[Light Node: Headers only / SPV]
    N_TYPES --> AN[Archive Node: Full state history]
    
    INFRA --> N_COMP(Internal Components):::component
    N_COMP --> Storage[(Database: LevelDB/RocksDB)]
    N_COMP --> EVM[Execution Environment: EVM/WASM]
    N_COMP --> Mempool[Mempool: Pending Tx Buffer]

    %% --- BRANCH 2: Peer-to-Peer (P2P) Network ---
    ROOT --- P2P[<b>II. P2P & Propagation</b>]:::layer
    P2P --> Discovery(Node Discovery):::component
    Discovery --> Bootnodes[Hardcoded Bootnodes]
    Discovery --> Kademlia[DHT / Peer Table]

    P2P --> Prop(Gossip Protocol):::component
    Prop --> Flood[Flooding: Tx Broadcasting]
    Prop --> BlockProp[Block Propagation & Inventory]
    
    P2P --- V_NET[<i>P2P Loopholes</i>]:::vuln
    V_NET --> V_Sybil(Sybil: Fake identity flood)
    V_NET --> V_Eclipse(Eclipse: Node isolation)
    V_NET --> V_DoS(Network-level DDoS)

    %% --- BRANCH 3: The Data Layer (Blocks & Chains) ---
    ROOT --- DATA[<b>III. The Data Layer</b>]:::layer
    DATA --> BlockHead(Block Header Metadata):::component
    BlockHead --> PrevHash[Previous Block Hash]
    BlockHead --> Merkle[Merkle Root: Tx Integrity]
    BlockHead --> Nonce[Nonce / Timestamp]

    DATA --> TxLogic(Transaction Models):::component
    TxLogic --> UTXO[UTXO: Bitcoin Style]
    TxLogic --> ACC[Account Based: Ethereum Style]
    
    DATA --- V_DATA[<i>Data Loopholes</i>]:::vuln
    V_DATA --> V_Malleability(Signature Malleability)
    V_DATA --> V_Replay(Transaction Replay)

    %% --- BRANCH 4: Consensus & Finality ---
    ROOT --- CONS[<b>IV. Consensus Mechanics</b>]:::layer
    CONS --> Mech(Algorithms):::component
    Mech --> PoW[Proof of Work: Hash Power]
    Mech --> PoS[Proof of Stake: Economic Bond]
    Mech --> BFT[pBFT / Tendermint: Voting]

    CONS --> Final(Finality Concepts):::component
    Final --> Prob[Probabilistic Finality]
    Final --> Det[Deterministic Finality]

    CONS --- V_CONS[<i>Consensus Loopholes</i>]:::vuln
    V_CONS --> V_51(51% Attack / Majority)
    V_CONS --> V_Selfish(Selfish Mining)
    V_CONS --> V_Long(Long Range Attacks)

    %% --- CROSS-FLOW: The Transaction Journey ---
    subgraph Journey [Transaction Lifecycle]
        T1[1. Signing: Private Key] --> T2[2. Broadcast: P2P]
        T2 --> T3[3. Validation: Node Rules]
        T3 --> T4[4. Mempool: Waiting]
        T4 --> T5[5. Inclusion: Mining/Staking]
        T5 --> T6[6. Confirmation: Immutability]
    end

    %% Connecting Lifecycle to Layers
    T2 -.-> P2P
    T4 -.-> Mempool
    T5 -.-> CONS
    T6 -.-> DATA

    %% Positioning
    style ROOT fill:#ffc300,color:#000
