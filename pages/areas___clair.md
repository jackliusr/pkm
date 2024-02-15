- an application for parsing image contents and reporting vulnerabilities affecting the contents. This is done via **static** analysis and not at runtime.
- clairctl
- [Architecture](https://quay.github.io/clair/whatis.html#architecture)
	- ![](https://quay.github.io/clair/clairv4_arch.png){:height 472, :width 384}
- [Modes](https://quay.github.io/clair/howto/getting_started.html#modes)
- [Indexer](https://quay.github.io/clair/reference/indexer.html), [matcher](https://quay.github.io/clair/reference/matcher.html), [notifier](https://quay.github.io/clair/reference/notifier.html) or combo mode. In combo mode, everything runs in a single OS process.
- [Claircore](https://quay.github.io/claircore/#claircore)
  
  ``` mermaid
  graph LR
  subgraph Indexer
  im[Image Manifest]
  libindex[Libindex]
  iir[IndexReport]
  im --> libindex --> iir
  end
  iir -.-> db[(Database)]
  ```
  ```mermaid
  graph LR
  subgraph Matcher
  mir[IndexReport]
  libvuln[Libvuln]
  vr[VulnerabilityReport]
  mir --> libvuln --> vr
  end
  db[(Database)] -.-> mir
  ```