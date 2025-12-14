# 🚀 Tempo Node - Docker Setup

Automated one-command setup for Tempo blockchain node using Docker.

## ⚡ Quick Start


# 1. Clone repository
```bash
git clone https://github.com/AirdropLaura/tempo-node.git
cd tempo-node
```
# 2. Run setup (installs Docker, pulls image, creates scripts)
```
chmod +x setup.sh
./setup.sh
```
# 3. Edit configuration with your credentials
```
nano ~/.tempo/.env
```
# Required changes:
# - CONSENSUS_SIGNING_KEY:   Your 64-char private key (NO 0x prefix)
# - CONSENSUS_FEE_RECIPIENT: Your wallet address (WITH 0x prefix)

# 4. Start node
```
cd ~/.tempo
./start.sh
```
# 5. Check status
```
./status.sh
```

## 📋 Requirements

- **OS:** Ubuntu 20.04+ / Debian 11+
- **RAM:** 4GB minimum (8GB recommended)
- **Storage:** 50GB+ SSD
- **Ports:** 8547, 8548, 30304

## 🔧 Configuration

After running `setup.sh`, edit `~/.tempo/.env`:

```bash
# Your 64-character private key (NO 0x prefix)
CONSENSUS_SIGNING_KEY=abc123def456...

# Your wallet address (WITH 0x prefix)
CONSENSUS_FEE_RECIPIENT=0x742d35Cc6634C0532925a3b844Bc454e4438f44e
```

⚠️ **IMPORTANT:**
- Private key must be 64 characters **WITHOUT** `0x` prefix
- Wallet address must be 42 characters **WITH** `0x` prefix

## 🎮 Usage

All commands are in `~/.tempo/`:

```bash
cd ~/.tempo

./start.sh      # Start node
./stop.sh       # Stop node
./restart.sh    # Restart node
./logs.sh       # View live logs (Ctrl+C to exit)
./status.sh     # Check node status
./test-rpc.sh   # Test RPC endpoints
./update.sh     # Update to latest version
./clean.sh      # Cleanup data
```

## 🌐 Endpoints

After starting the node: 

- **HTTP RPC:** `http://localhost:8547`
- **WebSocket:** `ws://localhost:8548`
- **P2P Port:** `30304`

### Test RPC

```bash
# Get latest block number
curl -X POST http://localhost:8547 \
  -H 'Content-Type: application/json' \
  -d '{"jsonrpc":"2.0","method":"eth_blockNumber","params":[],"id":1}'
```

Or use the built-in test script:

```bash
cd ~/.tempo
./test-rpc.sh
```

## 📊 Monitoring

### Check Status

```bash
cd ~/.tempo
./status.sh
```

Shows:
- Container status & uptime
- CPU & memory usage
- Port mappings
- Latest logs

### View Logs

```bash
cd ~/.tempo
./logs.sh  # Live logs (Ctrl+C to exit)
```

## 🐛 Troubleshooting

### Node won't start

```bash
# Check logs for errors
cd ~/.tempo
./logs.sh

# Verify configuration
cat ~/.tempo/.env
```

### Port already in use

Edit ports in `~/.tempo/.env`:

```bash
nano ~/.tempo/.env

# Change ports: 
TEMPO_HTTP_PORT=8548
TEMPO_WS_PORT=8549
TEMPO_P2P_PORT=30305

# Restart node
cd ~/.tempo
./restart.sh
```

### Reset everything

```bash
cd ~/.tempo
./clean.sh  # Choose option 3 for complete reset
./start.sh
```

### Update to latest version

```bash
cd ~/.tempo
./update.sh
```

## 📁 Directory Structure

```
~/.tempo/
├── . env              # Your configuration (DO NOT COMMIT!)
├── .env.example      # Template
├── . gitignore        # Git protection
├── start.sh          # Start node
├── stop.sh           # Stop node
├── restart.sh        # Restart node
├── logs.sh           # View logs
├── status.sh         # Check status
├── test-rpc.sh       # Test RPC
├── update.sh         # Update version
├── clean.sh          # Cleanup utility
├── data/             # Blockchain data
├── logs/             # Node logs
└── config/           # Key files
```

## 🔒 Security

### ⚠️ NEVER commit these files: 
- `.env` (contains your private key!)
- `config/signing-key.txt`
- `data/` directory
- `logs/` directory

The `.gitignore` is pre-configured to protect sensitive files.

### Best Practices

1. **Keep .env secure:**
   ```bash
   chmod 600 ~/.tempo/.env
   ```

2. **Backup . env safely:**
   ```bash
   cp ~/.tempo/.env ~/tempo-backup-$(date +%F).env
   ```

3. **Use firewall:**
   ```bash
   sudo ufw allow 8547/tcp  # HTTP RPC
   sudo ufw allow 8548/tcp  # WebSocket
   sudo ufw allow 30304/tcp # P2P
   ```

## 📚 Resources

- [Tempo Official Docs](https://docs.tempo.xyz)
- [GitHub Repository](https://github.com/tempoxyz/tempo)
- [Discord Community](https://discord.gg/tempo)

## 🆘 Support

Having issues? 

1. Check logs: `cd ~/.tempo && ./logs.sh`
2. Check status: `./status.sh`
3. Review this README
4. Visit [Tempo Documentation](https://docs.tempo.xyz)

## 📝 License

MIT License

---

**Made with ❤️ by AirdropLaura for the Tempo community**
