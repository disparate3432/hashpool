# Hashpool - Stratum V2 Reference Implementation Fork

This project is a fork of the Stratum V2 Reference Implementation (SRI) that replaces traditional share accounting with an ecash mint. For each mining share accepted by the pool, Hashpool generates "ehash", an ecash token backed by proof of work. Miners can hold choose to hold these tokens to maturity or trade them.

You can access the original SRI README [here](https://github.com/stratum-mining/stratum/blob/main/README.md).

## Getting Started

To run Hashpool, first **clone the repository** and follow the instructions to **[install nix and devenv](https://devenv.sh/getting-started/)**.

Once set up, cd into the hashpool directory and run:

```
devenv shell
devenv up
```

![Screenshot 2024-11-02 at 11 37 31 AM](https://github.com/user-attachments/assets/76b116b1-3aeb-4383-b67a-193740fc1b4b)

## Development Environment Setup

The development environment initializes a containerized system with the following components:

### Components Overview

1. **SV2 Mining Pool**
   - coordinates mining tasks and distributes workloads to miners
   - issues an ecash token for each share accepted
   - manages an internal cashu mint
      - receives a blinded message for each mining share
      - signs it and returns a blinded signature to the proxy/wallet

2. **SV2 Translator Proxy**
   - talks stratum v1 to downstream miners and stratum v2 to the upstream pool
   - manages the cashu wallet
      - bundles a blinded message with each share sent upstream to the pool
      - receives the blinded signature for each blinded message
      - stores each unblinded message with it's unblinded signature (this is an ecash token)

3. **SV2 Job Declarator Client**
   - talks to bitcoind miner side
   - retrieves block templates
   - negotiates work with upstream pool

4. **SV2 Job Declarator Server**
   - talks to bitcoind pool side
   - negotiates work with downstream proxy

5. **bitcoind (Sjors' SV2 Fork)**
   - modified bitcoind supporting stratum v2
   - check the [PR](https://github.com/bitcoin/bitcoin/pull/29432) for more information

6. **cpuminer**
   - find shares to submit upstream to the proxy

---

## Contribution

This project is very early. PRs and bug reports are very welcome!

---

