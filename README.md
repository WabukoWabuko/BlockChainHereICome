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
```

```mermaid
graph LR
    %% --- Theme & Styles (V2 Specific) ---
    classDef v2_core fill:#ff8c00,stroke:#000,color:#000,stroke-width:3px;
    classDef v2_layer fill:#fefae0,stroke:#dda15e,color:#000,stroke-width:1px;
    classDef v2_comp fill:#a8dadc,stroke:#457b9d,color:#000,stroke-width:1px;
    classDef v2_math fill:#457b9d,stroke:#1d3557,color:#fff,stroke-width:1px;
    classDef v2_vuln fill:#6a040f,stroke:#d00000,color:#fff,stroke-width:2px;

    %% --- Central Hub ---
    V2_ROOT((<b>VOLUME 2:<br/>The Cryptographic Vault</b>)):::v2_core

    %% --- BRANCH 1: Primitives & Math ---
    V2_ROOT --- V2_MATH[<b>I. Cryptographic Primitives</b>]:::v2_layer
    V2_MATH --> V2_Hash(Hashing Functions):::v2_comp
    V2_Hash --> V2_H1["Keccak-256 (EVM)"]:::v2_math
    V2_Hash --> V2_H2["SHA-256 (Bitcoin)"]:::v2_math
    V2_Hash --> V2_H3["RIPEMD-160 (Addresses)"]:::v2_math
    
    V2_MATH --> V2_Ecc(Elliptic Curve Cryptography):::v2_comp
    V2_Ecc --> V2_E1["Curve secp256k1 (Bitcoin/EVM)"]:::v2_math
    V2_Ecc --> V2_E2["Curve Ed25519 (Solana/Near)"]:::v2_math
    V2_Ecc --> V2_E3["Field Math: Modular Arithmetic"]:::v2_math
    V2_Ecc --> V2_E4["Scalar Multiplication / Point Addition"]:::v2_math

    V2_MATH --> V2_Sym(Symmetric Encryption):::v2_comp
    V2_Sym --> V2_AES["AES-256 (Keystore Encryption)"]:::v2_math

    V2_MATH --- V2_V_MATH[<i>Primitive Loopholes</i>]:::v2_vuln
    V2_V_MATH --> V2_M_Col(Hash Collisions)
    V2_V_MATH --> V2_M_Quan(Quantum Weakness)
    V2_V_MATH --> V2_M_Imp(Implementation Errors)

    %% --- BRANCH 2: Key Management Lifecycle ---
    V2_ROOT --- V2_KEYS[<b>II. Key & Identity Lifecycle</b>]:::v2_layer
    V2_KEYS --> V2_Gen(Generation Phase):::v2_comp
    V2_Gen --> V2_G1["Entropy Source: PRNG/HRNG"]:::v2_math
    V2_Gen --> V2_G2["BIP-39 Mnemonic / Seed Phrase"]
    V2_Gen --> V2_G3["BIP-32/44 HD Wallet Derivation"]:::v2_math

    V2_KEYS --> V2_Deriv(Derivation Path):::v2_comp
    V2_Deriv --> V2_D1[Master Private Key]
    V2_D1 --> V2_D2[Child Private Key]
    V2_D2 --> V2_D3["Public Key (Point G)"]:::v2_math
    V2_D3 --> V2_D4["Wallet Address (Keccak/RIPEMD)"]:::v2_math

    V2_KEYS --> V2_Storage(Storage Phase):::v2_comp
    V2_Storage --> V2_S1[Cold Storage - Air-gapped]
    V2_Storage --> V2_S2["Hardware Security Module (HSM)"]
    V2_Storage --> V2_S3[Hot Wallet - Software]
    V2_Storage --> V2_S4["Multi-Party Computation (MPC)"]
    
    V2_KEYS --- V2_V_KEYS[<i>Key Management Loopholes</i>]:::v2_vuln
    V2_V_KEYS --> V2_K_Ent(Weak Entropy Source)
    V2_V_KEYS --> V2_K_Path(Path Derivation Exploit)
    V2_V_KEYS --> V2_K_Clip(Clipboard Keyloggers)

    %% --- BRANCH 3: Transaction Signing (ECDSA) ---
    V2_ROOT --- V2_ECDSA[<b>III. Transaction Signing</b>]:::v2_layer
    V2_ECDSA --> V2_Sign(Signing Process):::v2_comp
    V2_Sign --> V2_Si1["Tx Payload / Message (m)"]
    V2_Sign --> V2_Si2["Hashing: H(m)"]:::v2_math
    V2_Sign --> V2_Si3["Generate Ephemeral Key (k)"]
    V2_Si4["Signature Components (r, s)"]:::v2_math
    V2_Si2 & V2_Si3 --> V2_Si4
    V2_Si4 --> V2_Si5["Broadcast Tx {m, r, s, PubKey}"]

    V2_ECDSA --> V2_Verif(Verification Process):::v2_comp
    V2_Verif --> V2_V1["Receive Tx Payload & Sig"]
    V2_V2["Reconstruct PubKey"]:::v2_math
    V2_Verif --> V2_V3["Check Verification Equation"]:::v2_math
    V2_V1 --> V2_V2
    V2_V2 --> V2_V3

    V2_ECDSA --- V2_V_ECDSA[<i>Signing Loopholes</i>]:::v2_vuln
    V2_V_ECDSA --> V2_E_Nonce(Nonce k Reuse Attack)
    V2_V_ECDSA --> V2_E_Rep(Replay - Lack of ChainID)
    V2_V_ECDSA --> V2_E_Mall(Signature Malleability)

    %% --- BRANCH 4: Advanced Concepts ---
    V2_ROOT --- V2_ADV[<b>IV. Advanced Cryptography</b>]:::v2_layer
    V2_ADV --> V2_Zkp(Zero-Knowledge Proofs):::v2_comp
    V2_Zkp --> V2_Z1[zk-SNARKs]
    V2_Zkp --> V2_Z2[zk-STARKs]
    
    V2_ADV --> V2_MpcA(MPC & TSS):::v2_comp
    V2_MpcA --> V2_M1[Threshold Signatures]
    V2_MpcA --> V2_M2[Key Sharding]

    V2_ADV --- V2_V_ADV[<i>Advanced Loopholes</i>]:::v2_vuln
    V2_V_ADV --> V2_A_ZkpF(ZKP Soundness Error)
    V2_V_ADV --> V2_A_Coll(Participant Collusion)
```

```mermaid
graph LR
    %% --- Theme & Styles (V3 Specific) ---
    classDef v3_core fill:#7209b7,stroke:#fff,color:#fff,stroke-width:3px;
    classDef v3_layer fill:#f72585,stroke:#fff,color:#fff,stroke-width:1px;
    classDef v3_comp fill:#4cc9f0,stroke:#000,color:#000,stroke-width:1px;
    classDef v3_evm fill:#3f37c9,stroke:#fff,color:#fff,stroke-width:1px;
    classDef v3_vuln fill:#6a040f,stroke:#d00000,color:#fff,stroke-width:2px;

    %% --- Central Hub ---
    V3_ROOT((<b>VOLUME 3:<br/>Smart Contract Internals</b>)):::v3_core

    %% --- BRANCH 1: The Compilation Pipeline ---
    V3_ROOT --- V3_COMP[<b>I. High-Level to Bytecode</b>]:::v3_layer
    V3_COMP --> V3_Lang(Languages):::v3_comp
    V3_Lang --> V3_L1[Solidity: Contract-Oriented]
    V3_Lang --> V3_L2[Vyper: Security-Centric / Pythonic]
    V3_Lang --> V3_L3[Huff/Yul: Low-Level Assembly]

    V3_COMP --> V3_Build(Build Artifacts):::v3_comp
    V3_Build --> V3_B1["ABI: Application Binary Interface (JSON)"]
    V3_Build --> V3_B2[Bytecode: Runtime vs Deployment]
    V3_Build --> V3_B3[Source Maps: Debugging Symbols]

    V3_COMP --- V3_V_COMP[<i>Compiler Loopholes</i>]:::v3_vuln
    V3_V_COMP --> V3_C_Ver(Compiler Version Bugs)
    V3_V_COMP --> V3_C_Opt(Optimizer Inconsistencies)

    %% --- BRANCH 2: EVM Architecture (The Virtual Machine) ---
    V3_ROOT --- V3_EVM[<b>II. EVM Architecture</b>]:::v3_layer
    V3_EVM --> V3_Memory(Volatile Memory):::v3_evm
    V3_Memory --> V3_M1["The Stack (1024 slots / 32 bytes)"]
    V3_Memory --> V3_M2["Memory (Linear Byte Array)"]
    V3_Memory --> V3_M3["Calldata (Read-only Input)"]

    V3_EVM --> V3_State(Persistent Storage):::v3_evm
    V3_State --> V3_S1["Storage Slots (Key-Value Mapping)"]
    V3_S2["Slot Packing (Gas Optimization)"]:::v3_comp
    V3_S1 --> V3_S2

    V3_EVM --> V3_Ops(Opcode Groups):::v3_evm
    V3_Ops --> V3_O1[Stack Ops: PUSH/POP/DUP/SWAP]
    V3_Ops --> V3_O2[Arithmetic: ADD/MUL/SUB/EXP]
    V3_Ops --> V3_O3[Context: CALLER/ADDRESS/GAS]
    V3_Ops --> V3_O4["Control: JUMP/JUMPI/REVERT"]

    V3_EVM --- V3_V_EVM[<i>EVM Loopholes</i>]:::v3_vuln
    V3_V_EVM --> V3_E_Stack(Stack Depth Limit - Pre-Spurious Dragon)
    V3_V_EVM --> V3_E_SColl(Storage Collision - Proxy Patterns)
    V3_V_EVM --> V3_E_OOB(Out-of-Bounds Memory Access)

    %% --- BRANCH 3: Contract Execution Flow ---
    V3_ROOT --- V3_FLOW[<b>III. Execution & Calls</b>]:::v3_layer
    V3_FLOW --> V3_Call(Call Types):::v3_comp
    V3_Call --> V3_C1["CALL (Standard External)"]
    V3_Call --> V3_C2["STATICCALL (Read-only)"]
    V3_Call --> V3_C3["DELEGATECALL (Context Sharing)"]

    V3_FLOW --> V3_Fall(Fallback Logic):::v3_comp
    V3_Fall --> V3_F1[receive: Handles Plain ETH]
    V3_Fall --> V3_F2[fallback: Handles Generic Calls]

    V3_FLOW --- V3_V_FLOW[<i>Logic Loopholes</i>]:::v3_vuln
    V3_V_FLOW --> V3_L_Re(Reentrancy - Inter-contract calls)
    V3_V_FLOW --> V3_L_Del(Delegatecall to Unstrusted Target)
    V3_V_FLOW --> V3_L_Gas(Gas Limit DoS)

    %% --- BRANCH 4: Gas Economics ---
    V3_ROOT --- V3_GAS[<b>IV. Gas & Incentives</b>]:::v3_layer
    V3_GAS --> V3_Calc(Gas Calculation):::v3_comp
    V3_Calc --> V3_G1[Base Fee + Priority Fee]
    V3_Calc --> V3_G2[Intrinsic Gas: 21,000]
    V3_Calc --> V3_G3[Computational Gas: Sum of Opcodes]

    V3_GAS --- V3_V_GAS[<i>Gas Loopholes</i>]:::v3_vuln
    V3_V_GAS --> V3_G_Grief(Gas Griefing Attacks)
    V3_V_GAS --> V3_G_Siphon(Unbounded Loop Siphoning)

    %% --- The "Stack Machine" Subgraph ---
    subgraph V3_StackMachine [EVM Processing Flow]
        V3_Proc1[1. Fetch Opcode] --> V3_Proc2[2. Decode & Execute]
        V3_Proc2 --> V3_Proc3[3. Update Stack/Storage]
        V3_Proc3 --> V3_Proc4{4. Check Gas}
        V3_Proc4 -- Enough --> V3_Proc1
        V3_Proc4 -- OOG --> V3_Proc5[REVERT / State Rollback]
    end
```

```mermaid
graph LR
    %% --- Theme & Styles (V4 Specific) ---
    classDef v4_core fill:#3a86ff,stroke:#fff,color:#fff,stroke-width:3px;
    classDef v4_layer fill:#8338ec,stroke:#fff,color:#fff,stroke-width:1px;
    classDef v4_comp fill:#ffbe0b,stroke:#000,color:#000,stroke-width:1px;
    classDef v4_econ fill:#06d6a0,stroke:#000,color:#000,stroke-width:1px;
    classDef v4_vuln fill:#6a040f,stroke:#d00000,color:#fff,stroke-width:2px;

    %% --- Central Hub ---
    V4_ROOT((<b>VOLUME 4:<br/>DeFi Economic Logic</b>)):::v4_core

    %% --- BRANCH 1: Automated Market Makers (AMM) ---
    V4_ROOT --- V4_AMM[<b>I. Liquidity & Exchanges</b>]:::v4_layer
    V4_AMM --> V4_Pools(Liquidity Pools):::v4_comp
    V4_Pools --> V4_P1["Constant Product: x * y = k (Uniswap v2)"]:::v4_econ
    V4_Pools --> V4_P2["Concentrated Liquidity (Uniswap v3)"]:::v4_econ
    V4_Pools --> V4_P3["Stablecoin Invariant (Curve)"]:::v4_econ

    V4_AMM --> V4_Mech(Mechanics):::v4_comp
    V4_Mech --> V4_M1[Slippage & Price Impact]
    V4_Mech --> V4_M2[Impermanent Loss]
    V4_Mech --> V4_M3[LP Token Mint/Burn]

    V4_AMM --- V4_V_AMM[<i>AMM Loopholes</i>]:::v4_vuln
    V4_V_AMM --> V4_V_Sandwich(Sandwich Attacks / MEV)
    V4_V_AMM --> V4_V_Imbalance(Pool Imbalance Exploits)

    %% --- BRANCH 2: Lending & Borrowing ---
    V4_ROOT --- V4_LEND[<b>II. Credit & Debt Markets</b>]:::v4_layer
    V4_LEND --> V4_Coll(Collateralization):::v4_comp
    V4_Coll --> V4_C1[Over-collateralized Loans]
    V4_Coll --> V4_C2[Loan-to-Value /LTV/ Ratios]
    V4_Coll --> V4_C3[Liquidation Thresholds]

    V4_LEND --> V4_Rate(Interest Rates):::v4_comp
    V4_Rate --> V4_R1[Utilization-based Rates]
    V4_Rate --> V4_R2[Supply vs Borrow APY]

    V4_LEND --- V4_V_LEND[<i>Lending Loopholes</i>]:::v4_vuln
    V4_V_LEND --> V4_V_BadDebt(Bad Debt Accumulation)
    V4_V_LEND --> V4_V_Liq(Liquidation Front-running)

    %% --- BRANCH 3: The Flash Loan Engine ---
    V4_ROOT --- V4_FLASH[<b>III. Atomic Composability</b>]:::v4_layer
    V4_FLASH --> V4_Atom(Atomic Transactions):::v4_comp
    V4_Atom --> V4_A1[Flash Loans: Zero Collateral]:::v4_econ
    V4_Atom --> V4_A2[Flash Swaps / Minting]
    V4_Atom --> V4_A3[Callback-driven Execution]

    V4_FLASH --- V4_V_FLASH[<i>Flash Loopholes</i>]:::v4_vuln
    V4_V_FLASH --> V4_V_Price(Flash Loan Price Manipulation)
    V4_V_FLASH --> V4_V_Gov(Governance Vote Buying)

    %% --- BRANCH 4: Price Oracles ---
    V4_ROOT --- V4_ORAC[<b>IV. External Data Feeds</b>]:::v4_layer
    V4_ORAC --> V4_Feed(Source Types):::v4_comp
    V4_Feed --> V4_O1[On-chain: TWAP / Uniswap]
    V4_Feed --> V4_O2[Off-chain: Chainlink / Pyth]
    V4_Feed --> V4_O3[Centralized: Exchange APIs]

    V4_ORAC --- V4_V_ORAC[<i>Oracle Loopholes</i>]:::v4_vuln
    V4_V_ORAC --> V4_V_Stale(Stale Price Feeds)
    V4_V_ORAC --> V4_V_Pump(Spot Price Manipulation)

    %% --- DEFI ATTACK VECTOR FLOW ---
    subgraph V4_ExploitFlow [Anatomy of a DeFi Hack]
        V4_X1[1. Flash Loan: Acquire massive capital] --> V4_X2[2. Manipulate: Skew AMM pool price]
        V4_X2 --> V4_X3[3. Trigger: Exploit Lending/Vault logic]
        V4_X3 --> V4_X4[4. Repay: Return loan + profit]
        V4_X4 --> V4_X5[5. Exit: Bridge funds to privacy mixer]
    end

    %% Linking the concepts
    V4_A1 -.-> V4_X1
    V4_P1 -.-> V4_X2
    V4_C3 -.-> V4_X3
```

```mermaid
graph LR
    %% --- Theme & Styles (V5 Specific) ---
    classDef v5_core fill:#ff006e,stroke:#fff,color:#fff,stroke-width:3px;
    classDef v5_layer fill:#3a0ca3,stroke:#fff,color:#fff,stroke-width:1px;
    classDef v5_comp fill:#4361ee,stroke:#fff,color:#fff,stroke-width:1px;
    classDef v5_infra fill:#4cc9f0,stroke:#000,color:#000,stroke-width:1px;
    classDef v5_vuln fill:#6a040f,stroke:#d00000,color:#fff,stroke-width:2px;

    %% --- Central Hub ---
    V5_ROOT((<b>VOLUME 5:<br/>Infrastructure & Bridges</b>)):::v5_core

    %% --- BRANCH 1: Cross-Chain Architectures ---
    V5_ROOT --- V5_ARCH[<b>I. Bridge Architectures</b>]:::v5_layer
    V5_ARCH --> V5_Type(Bridge Models):::v5_comp
    V5_Type --> V5_T1["Lock-and-Mint: Escrow on L1, Mint on L2"]
    V5_Type --> V5_T2["Burn-and-Redeem: Native Asset Swap"]
    V5_Type --> V5_T3["Liquidity Networks: Atomic Swaps"]

    V5_ARCH --> V5_Verify(Verification Methods):::v5_comp
    V5_Verify --> V5_V1["Native: Light Client on-chain"]
    V5_Verify --> V5_V2["External: Multi-sig / Validator Set"]
    V5_Verify --> V5_V3["Optimistic: Fraud Proof window"]

    V5_ARCH --- V5_V_ARCH[<i>Bridge Loopholes</i>]:::v5_vuln
    V5_V_ARCH --> V5_V_Mint(Infinite Mint Exploit)
    V5_V_ARCH --> V5_V_Proof(Faulty Merkle Proof Validation)

    %% --- BRANCH 2: Off-Chain Components (Relayers) ---
    V5_ROOT --- V5_OFF[<b>II. Relayers & Listeners</b>]:::v5_layer
    V5_OFF --> V5_Role(Operational Roles):::v5_comp
    V5_Role --> V5_R1[Event Listeners: Scanning Logs]
    V5_Role --> V5_R2[Message Passing: Cross-chain data]
    V5_Role --> V5_R3[Signature Aggregators]

    V5_OFF --- V5_V_OFF[<i>Relayer Loopholes</i>]:::v5_vuln
    V5_V_OFF --> V5_V_Sig(Signature Forgery)
    V5_V_OFF --> V5_V_Key(Relayer Private Key Theft)
    V5_V_OFF --> V5_V_Admin(Admin/Owner Account Takeover)

    %% --- BRANCH 3: Scaling & L2 Infrastructure ---
    V5_ROOT --- V5_L2[<b>III. Layer 2 & Rollups</b>]:::v5_layer
    V5_L2 --> V5_Roll(Rollup Types):::v5_comp
    V5_Roll --> V5_RL1[Optimistic: Arbitrum/Optimism]
    V5_Roll --> V5_RL2[zk-Rollup: ZKSync/Starknet]

    V5_L2 --> V5_Seq(Sequencer Node):::v5_comp
    V5_Seq --> V5_S1[Batch Submission to L1]
    V5_Seq --> V5_S2[Transaction Ordering]

    V5_L2 --- V5_V_L2[<i>Scaling Loopholes</i>]:::v5_vuln
    V5_V_L2 --> V5_V_L2C(Sequencer Centralization/Censorship)
    V5_V_L2 --> V5_V_Exit(L2 Withdrawal/Exit Scams)

    %% --- BRANCH 4: Web3 Infrastructure ---
    V5_ROOT --- V5_WEB3[<b>IV. Nodes & RPC Providers</b>]:::v5_layer
    V5_WEB3 --> V5_RPC(Access Points):::v5_comp
    V5_RPC --> V5_P1[Infura / Alchemy / QuickNode]
    V5_RPC --> V5_P2[Self-hosted / Specialized Nodes]

    V5_WEB3 --> V5_Store(Data Storage):::v5_comp
    V5_Store --> V5_ST1[IPFS: Content Addressing]
    V5_Store --> V5_ST2[Arweave: Permanent Storage]

    V5_WEB3 --- V5_V_WEB3[<i>Infra Loopholes</i>]:::v5_vuln
    V5_V_WEB3 --> V5_V_DNS(DNS Hijacking - Frontend)
    V5_V_WEB3 --> V5_V_API(RPC API Key Exposure)

    %% --- THE BRIDGE ATTACK LIFECYCLE ---
    subgraph V5_BridgeHack [Anatomy of a Bridge Exploit]
        V5_X1[1. Analysis: Identify Multi-sig threshold or Logic flaw] --> V5_X2[2. Action: Compromise Validator Keys or Forge Proofs]
        V5_X2 --> V5_X3[3. Execution: Submit fake 'Deposit' event to destination]
        V5_X3 --> V5_X4[4. Extraction: Mint/Withdraw native assets from Vault]
    end

    %% Linking the infrastructure to the hack
    V5_V2 -.-> V5_X2
    V5_R2 -.-> V5_X3
    V5_T1 -.-> V5_X4
```

```mermaid
graph LR
    %% --- Theme & Styles (V6 Specific) ---
    classDef v6_core fill:#00b4d8,stroke:#000,color:#000,stroke-width:3px;
    classDef v6_layer fill:#caf0f8,stroke:#0077b6,color:#000,stroke-width:1px;
    classDef v6_comp fill:#0077b6,stroke:#03045e,color:#fff,stroke-width:1px;
    classDef v6_tool fill:#90e0ef,stroke:#0077b6,color:#000,stroke-width:1px;
    classDef v6_vuln fill:#6a040f,stroke:#d00000,color:#fff,stroke-width:2px;

    %% --- Central Hub ---
    V6_ROOT((<b>VOLUME 6:<br/>The Auditor's Methodology</b>)):::v6_core

    %% --- BRANCH 1: Reconnaissance & Scoping ---
    V6_ROOT --- V6_RECON[<b>I. Recon & Preparation</b>]:::v6_layer
    V6_RECON --> V6_R1(Documentation Review):::v6_comp
    V6_R1 --> V6_R1_1[Whitepaper Analysis]
    V6_R1_2[Technical Spec & Flowcharts]
    
    V6_RECON --> V6_R2(Environment Setup):::v6_comp
    V6_R2 --> V6_R2_1["Tooling: Foundry / Hardhat"]:::v6_tool
    V6_R2_2["Dev Environment: Neovim / VS Code"]:::v6_tool
    V6_R2_3[Local Chain Forking: Anvil / Ganache]:::v6_tool

    %% --- BRANCH 2: Static Analysis (Automated) ---
    V6_ROOT --- V6_STATIC[<b>II. Static Analysis</b>]:::v6_layer
    V6_STATIC --> V6_S1(Security Tooling):::v6_comp
    V6_S1 --> V6_S1_1["Slither: Vulnerability Detection"]:::v6_tool
    V6_S1_2["Aderyn: Rust-based Static Analysis"]:::v6_tool
    V6_S1_3["Solhint: Linter & Best Practices"]:::v6_tool

    V6_STATIC --> V6_S2(Graphing & Visualization):::v6_comp
    V6_S2 --> V6_S2_1["Surya: Function Call Graphs"]:::v6_tool
    V6_S2_2[Solidity Visual Auditor]:::v6_tool

    %% --- BRANCH 3: Manual Code Review ---
    V6_ROOT --- V6_MANUAL[<b>III. Manual Code Review</b>]:::v6_layer
    V6_MANUAL --> V6_M1(Top-Down Analysis):::v6_comp
    V6_M1 --> V6_M1_1[Entry Point: External/Public Functions]
    V6_M1_2[State Transitions: SSTORE Analysis]
    
    V6_MANUAL --> V6_M2(Logic Verification):::v6_comp
    V6_M2 --> V6_M2_1[Access Control: Modifiers check]
    V6_M2_2[Math Safety: Overflows/Rounding]
    V6_M2_3[External Calls: Reentrancy checks]

    %% --- BRANCH 4: Dynamic Analysis (Testing) ---
    V6_ROOT --- V6_DYN[<b>IV. Dynamic Testing</b>]:::v6_layer
    V6_DYN --> V6_D1(Fuzzing):::comp
    V6_D1 --> V6_D1_1["Echidna: Property-based Fuzzing"]:::v6_tool
    V6_D1_2["Foundry: Invariant Testing"]:::v6_tool
    
    V6_DYN --> V6_D2(Exploit Development):::v6_comp
    V6_D2 --> V6_D2_1[PoC Development: Hardhat/Foundry]
    V6_D2_2[Mainnet Forking: Testing against live state]

    %% --- BRANCH 5: Reporting & Disclosure ---
    V6_ROOT --- V6_REPORT[<b>V. Finalization</b>]:::v6_layer
    V6_REPORT --> V6_P1(Severity Classification):::v6_comp
    V6_P1 --> V6_P1_1[High: Direct loss of funds]:::v6_vuln
    V6_P1_2[Medium: Logic error / Protocol grief]
    V6_P1_3[Low/Gas: Optimization / Non-critical]

    V6_REPORT --> V6_P2(Reporting):::v6_comp
    V6_P2 --> V6_P2_1[Description & Impact]
    V6_P2_2[Proof of Concept - PoC]
    V6_P2_3[Recommended Remediation]

    %% --- THE AUDIT LOOP ---
    subgraph V6_AuditPipeline [The Auditor's Daily Workflow]
        V6_Step1[1. Understand System Goals] --> V6_Step2[2. Run Static Analysis]
        V6_Step2 --> V6_Step3[3. Manual Line-by-Line Review]
        V6_Step3 --> V6_Step4[4. Write Invariant Tests/Fuzzers]
        V6_Step4 --> V6_Step5[5. Draft & Submit Report]
    end
```
