# 🏎️ Formula-1 Fan Token Exchange (F1FanTokenExchange)

**A secure, audited, and decentralized reward exchange for Formula-1 fans.**  
This smart contract enables F1 teams, communities, or organizations to distribute **on-chain fan engagement rewards** while ensuring **DeFi-grade security** and **MEV-resistant behavior.**

---

## 🔐 Overview

The **F1FanTokenExchange** is a fully self-contained Solidity contract designed for maximum security and audit compliance.  
It enables:

- 🪙 **Fan registration & reward tracking**  
- 🎁 **Token-based engagement rewards**  
- 🧱 **MEV protection** using block-based claim spacing  
- ⛔ **Anti-reentrancy**, **pausing**, and **safe transfer checks**  
- 👑 **Two-step ownership** for safer admin transitions  

This contract is written under **Solidity 0.8.20** with all major vulnerability classes addressed.

---

## 🧠 Architecture

| Layer | Purpose | Security Features |
|-------|----------|-------------------|
| **ERC20 Interface** | Minimal token interface | No external imports |
| **SafeERC20 Library** | Secure wrapper for token transfers | Prevents unchecked transfer vulnerabilities |
| **Ownable2Step** | Secure two-step ownership transfer | Prevents accidental ownership loss |
| **ReentrancyGuard** | Prevents reentrancy attacks | Simple non-reentrant modifier |
| **Pausable** | Emergency circuit breaker | Controlled by owner |
| **Main Contract (F1FanTokenExchange)** | Core logic for fan reward assignment & claiming | Includes anti-MEV logic, zero-address checks, capped rewards |

---

## 🧰 Key Features

- ✅ **Full Reentrancy Protection** using `nonReentrant`
- ✅ **SafeERC20 Transfers** (no unchecked low-level calls)
- ✅ **Zero-Value and Zero-Address Checks**
- ✅ **Pragma Locked (0.8.20)** for compiler stability
- ✅ **Owner-Controlled Emergency Pause**
- ✅ **MEV-Defense**: Requires `minBlockSpacing` between claims
- ✅ **Max Reward Cap** to prevent over-distribution
- ✅ **Two-Step Ownership Transfer** for audit-safe admin changes

---

## ⚙️ Deployment Parameters

| Parameter | Type | Description |
|------------|------|-------------|
| `_fanToken` | `IERC20` | (Optional) The fan engagement token |
| `_rewardToken` | `IERC20` | The ERC-20 token used for rewards |
| `_initialRewardPool` | `uint256` | Initial pool balance (must be deposited) |
| `_maxRewardPerClaim` | `uint256` | Reward cap per fan claim |
| `_minBlockSpacing` | `uint256` | Block spacing between user claims (anti-MEV) |

**Constructor Example:**
```solidity
constructor(
    IERC20 _fanToken,
    IERC20 _rewardToken,
    uint256 _initialRewardPool,
    uint256 _maxRewardPerClaim,
    uint256 _minBlockSpacing
) payable Ownable2Step(msg.sender) ReentrancyGuard() Pausable() {}
