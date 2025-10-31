#!/usr/bin/env python3
# xpomocoma_osint.py
# Author: xpomocomaxakepa-hack
# Real OSINT tool: checks if public accounts exist

import requests
import time
import sys

# Colors
GREEN = "\033[32m"
YELLOW = "\033[33m"
CYAN = "\033[36m"
RESET = "\033[0m"

HEADERS = {"User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64)"}

def slow_print(text: str, delay: float = 0.03) -> None:
    """Print text character by character with delay."""
    for c in text:
        print(c, end='', flush=True)
        time.sleep(delay)
    print()

def check_url(url: str) -> bool:
    """Check if a URL exists."""
    try:
        response = requests.get(url, headers=HEADERS, timeout=5)
        return response.status_code == 200
    except requests.RequestException:
        return False

def display_result(platform: str, url: str, exists: bool) -> None:
    """Print result of account check with colors."""
    if exists:
        slow_print(f"{GREEN}[+] {platform} account found: {url}{RESET}")
    else:
        slow_print(f"{YELLOW}[-] {platform} account not found{RESET}")

def osint_accounts(username: str) -> None:
    """Check public accounts and website info for the given username."""
    slow_print(f"\n{CYAN}XPOMOCOMA osinting {username}...{RESET}\n")
    
    platforms = {
        "GitHub": f"https://github.com/{username}",
        "Instagram": f"https://www.instagram.com/{username}/",
        "TikTok": f"https://www.tiktok.com/@{username}",
        "Twitter": f"https://twitter.com/{username}",
        "YouTube": f"https://www.youtube.com/@{username}",
        "Telegram": f"https://t.me/{username}"
    }

    for platform, url in platforms.items():
        display_result(platform, url, check_url(url))
    
    # Check if input looks like a website
    if username.startswith(("http://", "https://")):
        try:
            response = requests.head(username, headers=HEADERS, timeout=5)
            slow_print(f"\n{GREEN}Website Info:{RESET}")
            slow_print(f"URL: {username}")
            slow_print(f"Status Code: {response.status_code}")
            slow_print(f"Server: {response.headers.get('Server', 'Unknown')}")
        except requests.RequestException:
            slow_print(f"{YELLOW}Failed to fetch website info{RESET}")

def main_menu() -> None:
    """Main interactive menu loop."""
    while True:
        slow_print(f"{CYAN}Welcome to XPOMOCOMA XAKEPA OSINT Tool!{RESET}\n")
        slow_print("Select an option:\n1 - Start OSINT\n2 - Exit\n")
        choice = input("Your choice: ").strip()
        
        if choice == "1":
            target = input("\nEnter target username or website: ").strip()
            osint_accounts(target)
            input("\nPress Enter to return to menu...")
        elif choice == "2":
            slow_print(f"\n{GREEN}Exiting XPOMOCOMA OSINT. Stay curious!{RESET}")
            sys.exit(0)
        else:
            slow_print(f"{YELLOW}Invalid choice. Try again.{RESET}\n")

if __name__ == "__main__":
    main_menu()
