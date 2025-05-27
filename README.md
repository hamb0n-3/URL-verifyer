# Stealthy URL Status Checker (Red Team Edition)

A multi-threaded, stealthy URL status checker designed for red teamers, penetration testers, and OSINT professionals. This tool checks the status of URLs with anti-blocking techniques, user-agent rotation, optional proxy chaining, and can respect API rate limits.

## Features
- Multi-threaded scanning for speed
- User-agent rotation to evade detection
- Proxy chaining support (optional)
- SSL verification control
- Verbose progress reporting
- Anti-blocking random delays
- Optional rate limit handling for APIs
- CSV output with full diagnostics

## Usage

```sh
python3 URL-verifyer.py -i urls.txt [options]
```

### Required Arguments
- `-i, --input`   Input file containing URLs (one per line)

### Optional Arguments
- `-o, --output`      Output CSV file (default: `results.csv`)
- `-t, --threads`     Number of concurrent threads (default: 1)
- `-p, --proxies`     File containing proxy servers (default: `proxies.txt`)
- `-d, --delay`       Delay range between requests in seconds (default: 1 4)
- `--verify-ssl`      Enable SSL certificate verification
- `-v, --verbose`     Enable verbose output
- `--rate-limit`      Respect X-RateLimit headers if present (for APIs)

## Example Commands

Basic scan:
```sh
python3 URL-verifyer.py -i urls.txt
```

Verbose, multi-threaded scan with 10 threads:
```sh
python3 URL-verifyer.py -i urls.txt -t 10 -v
```

Scan using proxies and respect API rate limits:
```sh
python3 URL-verifyer.py -i urls.txt -p myproxies.txt --rate-limit
```

## Proxy Support
- Place your proxies (one per line) in a file (default: `proxies.txt`).
- Supported formats: `http://host:port`, `socks5://host:port`, etc.

## Rate Limiting (APIs)
- If `--rate-limit` is enabled, the tool will respect `X-RateLimit-Remaining` and `X-RateLimit-Reset` headers (if present) and sleep as needed.
- Useful for scanning APIs like GitHub, Twitter, etc.

## Output
- Results are saved in CSV format with columns: timestamp, url, status, error, ip, attempts, proxy, user_agent.

## Red Team Notes
- Randomized user-agents and delays help evade basic detection and blocking.
- Proxy support allows for chaining and IP rotation.
- Respecting rate limits helps avoid bans when targeting APIs.
- Use responsibly and only on targets you are authorized to test.

## Requirements
- Python 3.x
- `requests`, `urllib3` (install via `pip install -r requirements.txt` if needed)

---

*For educational and authorized testing only.* 