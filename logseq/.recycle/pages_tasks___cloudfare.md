- ``` mermaid
  flowchart TD
      start[Start] -->point1{Transfer?}
      point1 -->|yes, need to verify if cloudflare support ccTLD sg| transer[Transfer DNS\nto Cloudflare] 
      point1 -->|No| nameserver[Change DNS nameserver point \nto cloudflare]
      transer-->Cloudflare
      nameserver-->Cloudflare
      Cloudflare-->|www|www(www cname to \naws,azure)
      Cloudflare-->|apex|pagerule[Page Rules redirect to www]
      www -->END
      pagerule-->END
      classDef highlight stroke:#f00
  ```
-