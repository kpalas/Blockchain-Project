# Blockchain-Project
Blockchain
A simple blockchain implementation in Java that demonstrates the core concepts of cryptocurrency transactions, digital signatures, and proof-of-work mining.
Overview
This project implements a basic cryptocurrency system with the following features:

Wallet creation with public/private key pairs
Digital signatures using ECDSA (Elliptic Curve Digital Signature Algorithm)
Transaction creation and validation
UTXO (Unspent Transaction Output) model
Proof-of-work mining algorithm
Merkle tree implementation for transaction verification
Blockchain validation

#Project Structure
├── blockchain.java          # Main blockchain class and entry point
├── block.java              # Block implementation with mining
├── Wallet.java             # Wallet with key generation and transaction sending
├── Transaction.java        # Transaction processing and validation
├── TransactionInput.java   # Transaction input references
├── TransactionOutput.java  # Transaction output implementation
└── StringUtil.java         # Utility functions (hashing, signatures, Merkle root)Components
Blockchain (blockchain.java)

Main entry point of the application
Manages the blockchain data structure
Maintains global UTXO set
Validates blockchain integrity
Controls mining difficulty

Block (block.java)

Contains list of transactions
Implements proof-of-work mining
Calculates block hash using SHA-256
Generates Merkle root for transactions
Links to previous block via hash

Wallet (Wallet.java)

Generates ECDSA key pairs (192-bit prime curve)
Tracks wallet balance via UTXOs
Creates and signs transactions
Manages owned transaction outputs

Transaction (Transaction.java)

Processes cryptocurrency transfers
Validates transaction signatures
Manages inputs and outputs
Enforces minimum transaction rules
Updates global UTXO set

Transaction I/O

TransactionInput: References unspent outputs to be consumed
TransactionOutput: Creates new outputs with recipient and value

Utilities (StringUtil.java)

SHA-256 hashing
ECDSA signature generation and verification
Merkle tree root calculation
Key encoding utilities

Dependencies

Bouncy Castle (org.bouncycastle.jce.provider.BouncyCastleProvider) - Cryptographic operations
Gson (com.google.gson.GsonBuilder) - JSON serialization (optional)

How It Works
1. Key Generation
Each wallet generates an ECDSA key pair using the prime192v1 curve for signing transactions.
2. Genesis Transaction
The blockchain starts with a genesis transaction that creates the initial supply of NoobCoins (100 coins to walletA).
3. Transaction Flow

Sender checks balance against UTXOs
Transaction inputs reference previous unspent outputs
Transaction is signed with sender's private key
Transaction creates new outputs (recipient + change)
Signature is verified using sender's public key
Valid transactions are added to blocks

4. Mining
Blocks are mined using proof-of-work:

Difficulty level determines required leading zeros
Nonce is incremented until valid hash is found
Merkle root ensures transaction integrity

5. Validation
The blockchain validates:

Hash integrity of each block
Proper linking between blocks
Mining difficulty compliance
Transaction signatures
UTXO availability

Running the Project
Prerequisites
bash# Add Bouncy Castle JAR to classpath
# Download from: https://www.bouncycastle.org/latest_releases.html
Compilation
bashjavac -cp ".:bcprov-jdk15on-*.jar" *.java
Execution
bashjava -cp ".:bcprov-jdk15on-*.jar" blockchain
Configuration
Key parameters in blockchain.java:

difficulty = 5 - Mining difficulty (number of leading zeros)
minimumTransaction = 0.1f - Minimum transaction value

Example Output
Creating and Mining Genesis block...
Block Mined!!: 00000a1b2c3d...
Transaction Successfully added to Block

WalletA's balance is: 100.0

WalletA is Attempting to send funds (40) to WalletB...
Block Mined!!: 00000e4f5g6h...
Transaction Successfully added to Block

WalletA's balance is: 60.0
WalletB's balance is: 40.0
Security Features

ECDSA Signatures: Prevents transaction tampering and ensures authenticity
SHA-256 Hashing: Cryptographically secure block linking
UTXO Model: Prevents double-spending
Merkle Trees: Efficient transaction verification
Proof-of-Work: Prevents blockchain manipulation

Limitations
This is an educational implementation with several simplifications:

No network/peer-to-peer functionality
No transaction fees
Single-threaded mining
In-memory storage only
Simplified UTXO management
No script system for advanced transactions

Known Issues to Fix
Before running, ensure you fix:

block.java - Add merkleRoot field
Transaction.java - Fix typo: calulateHash() → calculateHash()
TransactionOutput.java - Use .equals() instead of == for PublicKey comparison
StringUtil.java - Add getDificultyString() method
blockchain.java - Add addBlock() method

Future Enhancements

Implement networking for distributed blockchain
Add transaction pool/mempool
Implement transaction fees
Add wallet persistence
Create REST API
Add blockchain explorer interface
Implement SPV (Simplified Payment Verification)

Learning Resources
This project demonstrates:

Blockchain fundamentals
Cryptocurrency transaction models
Cryptographic signatures
Proof-of-work consensus
Hash-based data structures

License
Educational project - free to use and modify.
