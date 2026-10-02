# mta-sts.finever.com

finever.com için MTA-STS politikası (RFC 8461), GitHub Pages ile yayınlanır:
https://mta-sts.finever.com/.well-known/mta-sts.txt

- Politika satırları CRLF ile ayrılır (`.gitattributes` korur).
- `.nojekyll` olmadan Jekyll `.well-known` klasörünü yayınlamaz.
- Politika her değiştiğinde DNS'teki `_mta-sts.finever.com` TXT kaydındaki `id` de değişmeli
  (ör. `v=STSv1; id=20261002`), yoksa gönderen sunucular eski politikayı önbellekten kullanır.

## DNS (Natro)

| Tür   | Ad          | Değer                                         |
|-------|-------------|-----------------------------------------------|
| CNAME | mta-sts     | finevertech.github.io                         |
| TXT   | _mta-sts    | v=STSv1; id=20261002                          |
| TXT   | _smtp._tls  | v=TLSRPTv1; rua=mailto:dmarc@finever.com      |

## Testing → enforce

Birkaç hafta TLS-RPT raporları temiz gelirse `mode: enforce` ve `max_age: 604800` yapılır,
`_mta-sts` kaydının `id`'si yenilenir.
