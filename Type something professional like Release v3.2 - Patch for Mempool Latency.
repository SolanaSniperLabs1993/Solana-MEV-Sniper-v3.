#!/usr/bin/env python3
import time
import random
import sys
from datetime import datetime

# Try to use colorama on Windows; otherwise fall back to ANSI codes.
try:
    from colorama import init, Fore, Style
    init(autoreset=True)
    GREEN = Fore.GREEN
    YELLOW = Fore.YELLOW
    CYAN = Fore.CYAN
    RED = Fore.RED
    MAGENTA = Fore.MAGENTA
    RESET = Style.RESET_ALL
except Exception:
    GREEN = '\033[92m'
    YELLOW = '\033[93m'
    CYAN = '\033[96m'
    RED = '\033[91m'
    MAGENTA = '\033[95m'
    RESET = '\033[0m'

DELAY_MIN = 0.10
DELAY_MAX = 0.30

def rnd_delay():
    time.sleep(random.uniform(DELAY_MIN, DELAY_MAX))

def line(text, color=None, end='\n'):
    prefix = ''
    suffix = RESET
    if color:
        prefix = color
    else:
        suffix = ''
    sys.stdout.write(f"{prefix}{text}{suffix}{end}")
    sys.stdout.flush()
    rnd_delay()

def banner(msg, color=GREEN):
    width = max(60, len(msg) + 10)
    line_top = '#' * width
    padding = (width - len(msg) - 2) // 2
    middle = '#{}{}{}#'.format(' ' * padding, msg, ' ' * (width - len(msg) - 2 - padding))
    line(line_top, color)
    line(middle, color)
    line(line_top, color)

def hex_id(n=8):
    return ''.join(random.choice('0123456789abcdef') for _ in range(n))

def fmt_amount(n):
    return f"${n:,.2f}"

def simulate():
    # Header
    banner("HIGH-FREQUENCY TRADING - SIMULATION", color=CYAN)

    line(f"[{datetime.now().isoformat()}] INIT: Booting simulated Solana node...", CYAN)
    node = f"sol-node-{hex_id(6)}"
    line(f"[{datetime.now().isoformat()}] NODE: {node} (status: LISTENING)", CYAN)

    # Connecting
    line("-> Establishing P2P connections...", YELLOW)
    for i in range(3):
        peers = random.randint(20, 120)
        line(f"   - Peers connected: {peers}", YELLOW)
    line("-> Synchronizing ledger headers...", YELLOW)
    for p in range(0, 101, 25):
        line(f"   - headers sync {p}%", YELLOW)

    # Mempool scanning
    mempool_items = random.randint(150, 450)
    line(f"[{datetime.now().isoformat()}] MEMPOOL: scanning {mempool_items} txs for arbitrage/sniping targets...", YELLOW)
    scan_steps = random.randint(6, 12)
    for i in range(scan_steps):
        pct = int((i + 1) / scan_steps * 100)
        sample_ht = hex_id(12)
        line(f"   [SCAN] {pct}% - checking tx {sample_ht} ...", YELLOW)

    # Found potential target
    target_token = random.choice(["NEON", "RUSH", "GLXY", "SYNTH", "QUANTX"])
    target_score = random.uniform(0.78, 0.999)
    line(f"[{datetime.now().isoformat()}] ALERT: potential target found -> {target_token}", GREEN)
    line(f"   - Opportunity score: {target_score:.3f}", GREEN)
    line(f"   - Estimated slippage tolerance: {random.uniform(0.2, 1.5):.2f}%", GREEN)

    # Lock on target
    target_addr = "0x" + hex_id(40)
    line(f"-> LOCK: locking sniper session on token {target_token} @ {target_addr}", CYAN)
    line("-> Preparing signed payload (simulated)...", CYAN)
    for i in range(4):
        line(f"   - nonce {hex_id(8)} signed", CYAN)

    # Pre-execution checks
    line("-> Pre-execution checks:", CYAN)
    checks = [
        ("latency", f"{random.uniform(4.0, 18.0):.2f}ms"),
        ("estimated_fee", fmt_amount(random.uniform(2.0, 25.0))),
        ("front_run_risk", f"{random.uniform(0.0, 0.3):.2%}"),
        ("rpc_health", "OK")
    ]
    for k, v in checks:
        color = GREEN if k != "front_run_risk" else (YELLOW if float(v.strip('%'))/100 < 0.1 else RED)
        # Keep color logic simple and safe for formatting
        line(f"   - {k:15}: {v}", GREEN if k != "front_run_risk" else YELLOW)

    # Execute "Sniper Trade" (simulated)
    line(f"[{datetime.now().isoformat()}] EXECUTE: launching sniper trade...", MAGENTA)
    txid = hex_id(64)
    line(f"   -> raw_tx_id: {txid}", MAGENTA)
    confirmations_needed = random.randint(1, 3)
    for c in range(confirmations_needed):
        line(f"   -> broadcasted (attempt {c+1}) ...", MAGENTA)

    # Outcome
    success = random.choices([True, False], weights=[0.9, 0.1])[0]
    if success:
        profit = random.uniform(120000.0, 9_000_000.0)
        pnl = fmt_amount(profit)
        slippage = random.uniform(0.05, 0.9)
        line(f"   -> trade_status: EXECUTED", GREEN)
        line(f"   -> realized_profit: {pnl}", GREEN)
        line(f"   -> slippage_actual: {slippage:.2f}%", GREEN)
        line(f"   -> tx_confirmed: {random.randint(1, 6)} blocks", GREEN)
    else:
        line(f"   -> trade_status: FAILED (reverted)", RED)
        line(f"   -> reason: insufficient liquidity / slippage exceeded", RED)
        line(f"   -> rollback complete", RED)

    # Final banner
    if success:
        banner("PROFIT SECURED", color=GREEN)
        line(f"[{datetime.now().isoformat()}] SESSION END: sniper session {node} closed.", CYAN)
    else:
        banner("SESSION ABORTED", color=RED)
        line(f"[{datetime.now().isoformat()}] SESSION END: no profit realized.", CYAN)

if __name__ == "__main__":
    simulate()
