# DNS-Resolver-Benchmark

A versatile DNS resolver benchmarking script supporting traditional DNS, DNS-over-HTTPS (DoH), DNS-over-TLS (DoT), DNS-over-QUIC (DoQ), and DNSCrypt, with detailed performance reporting.

## Features

- Support for multiple DNS protocols:
  - Traditional DNS (IP addresses)
  - DNS-over-HTTPS (DoH)
  - DNS-over-TLS (DoT)
  - DNS-over-QUIC (DoQ)
  - DNSCrypt
- Concurrent DNS resolution testing
- Detailed performance metrics:
  - Response times (average, min, max, standard deviation)
  - Error rates
  - Success/failure counts
- Excel report generation with:
  - Color-coded performance indicators
  - Server-wise summary statistics
  - Comprehensive error reporting

## Requirements

- Python 3.6 or higher
- `dnslookup.exe` executable in the script directory (see [Binary Verification](#binary-verification))
- Required Python packages:
  ```
  openpyxl
  pandas
  colorama
  ```

## Binary Verification

This project uses `dnslookup` v1.11.1 (32-bit) binary from [ameshkov/dnslookup](https://github.com/ameshkov/dnslookup). 

Required binary: `dnslookup-windows-386-v1.11.1.zip`
MD5 checksum: `96EC86CCEE7D3B55FF078C773B4BDF5D`

You can verify the checksum using:
```bash
# Windows (PowerShell)
Get-FileHash -Algorithm MD5 dnslookup.exe

# Windows (Command Prompt)
certutil -hashfile dnslookup.exe MD5
```

To download the binary:
1. Visit [dnslookup v1.11.1 release](https://github.com/ameshkov/dnslookup/releases/tag/v1.11.1)
2. Download `dnslookup-windows-386-v1.11.1.zip`
3. Extract the ZIP file and place `dnslookup.exe` in the script directory

## Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/ramhaidar/DNS-Resolver-Benchmark.git
   cd DNS-Resolver-Benchmark
   ```

2. Install required packages:
   ```bash
   pip install openpyxl pandas colorama
   ```

3. Download `dnslookup.exe` and place it in the script directory.

## Configuration

### Test Domains
Create a `test_domains.txt` file with domains to test (one per line). Example content:
```
# Popular sites
google.com
youtube.com
facebook.com
twitter.com
instagram.com

# Tech sites
github.com
stackoverflow.com
gitlab.com

# CDN providers
cloudflare.com
akamai.com
fastly.com

# Local sites
detik.com
kompas.com
tokopedia.com
```

### DNS Servers
Create a `dns_servers.txt` file with DNS servers to test (one per line). Example content:
```
# Traditional DNS (IP address format)
8.8.8.8             # Google DNS
8.8.4.4             # Google DNS Secondary
1.1.1.1             # Cloudflare DNS
1.0.0.1             # Cloudflare DNS Secondary
9.9.9.9             # Quad9
149.112.112.112     # Quad9 Secondary

# DNS-over-TLS (DoT)
tls://1.1.1.1:853                   # Cloudflare
tls://8.8.8.8:853                   # Google
tls://dns.quad9.net:853             # Quad9
tls://dns.adguard.com:853           # AdGuard
tls://dot.sb:853                    # ControlD

# DNS-over-HTTPS (DoH)
https://cloudflare-dns.com/dns-query # Cloudflare
https://dns.google/dns-query         # Google
https://doh.opendns.com/dns-query    # OpenDNS
https://dns.quad9.net/dns-query      # Quad9
https://dns.adguard.com/dns-query    # AdGuard

# DNS-over-QUIC (DoQ)
quic://dns.adguard.com:853          # AdGuard
quic://dns.quad9.net:853            # Quad9
quic://cloudflare-dns.com:853       # Cloudflare
```

### Configuration Parameters
Modify the CONFIG dictionary in `main.py` to adjust:
```python
CONFIG = {
    "NUM_QUERIES": 30,        # Queries per domain-server pair
    "DOMAINS_FILE": "test_domains.txt",
    "DNS_SERVERS_FILE": "dns_servers.txt",
    "DNSLOOKUP_EXE": "dnslookup.exe",
    "MAX_THREADS": 1,         # Concurrent resolution threads
}
```

## Usage

Run the benchmark:
```bash
python main.py
```

The script will:
1. Validate configuration and dependencies
2. Perform DNS resolution tests
3. Display real-time progress
4. Show detailed results in the console
5. Generate an Excel report (`dns_server_performance_TIMESTAMP.xlsx`)

## Output

### Console Output
- Real-time progress indicator
- Per-domain, per-server resolution results
- Response times and resolved IP addresses

### Excel Report
- Server performance summary
- Response time statistics
- Error rates and messages
- Color-coded performance indicators:
  - Green: Low error rate (≤10%)
  - Yellow: Moderate error rate (≤50%)
  - Red: High error rate (>50%)
  - Gray: Not working

## Credits

- DNS lookup functionality powered by [dnslookup](https://github.com/ameshkov/dnslookup) by [@ameshkov](https://github.com/ameshkov)

## License

[MIT License](LICENSE)

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.
