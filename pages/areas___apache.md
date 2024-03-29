- [Apache Module mod_rewrite](https://httpd.apache.org/docs/2.4/mod/mod_rewrite.html)
	- RewriteBase *URL-path*
	- RewriteCond *TestString* *CondPattern* [*flags*]
	- RewriteEngine on|off
	- RewriteMap *MapName* *MapType*:*MapSource* [*MapTypeOptions*]
	- RewriteOptions Options
	- RewriteRule *Pattern* *Substitution* [*flags*]
		- [RewriteRule Flags](https://httpd.apache.org/docs/2.4/rewrite/flags.html)
			- **RewriteRule** pattern target [Flag1,Flag2,Flag3]
			- flags:
				- [B (escape backreferences)](https://httpd.apache.org/docs/2.4/rewrite/flags.html#flag_b)
				- [BNP|backrefnoplus (don't escape space to +)](https://httpd.apache.org/docs/2.4/rewrite/flags.html#flag_bnp)
				- [BCTLS](https://httpd.apache.org/docs/2.4/rewrite/flags.html#flag_bctls)
				- [BNE](https://httpd.apache.org/docs/2.4/rewrite/flags.html#flag_bne)
				- [C|chain](https://httpd.apache.org/docs/2.4/rewrite/flags.html#flag_c)
				- [CO|cookie](https://httpd.apache.org/docs/2.4/rewrite/flags.html#flag_co)
				- [DPI|discardpath](https://httpd.apache.org/docs/2.4/rewrite/flags.html#flag_dpi)
				- [E|env](https://httpd.apache.org/docs/2.4/rewrite/flags.html#flag_e)
				- [END](https://httpd.apache.org/docs/2.4/rewrite/flags.html#flag_end)
				- [F|forbidden](https://httpd.apache.org/docs/2.4/rewrite/flags.html#flag_f)
				- [G|gone](https://httpd.apache.org/docs/2.4/rewrite/flags.html#flag_g)
				- [H|handler](https://httpd.apache.org/docs/2.4/rewrite/flags.html#flag_h)
				- [L|last](https://httpd.apache.org/docs/2.4/rewrite/flags.html#flag_l)
				- [N|next](https://httpd.apache.org/docs/2.4/rewrite/flags.html#flag_n)
				- [NC|nocase](https://httpd.apache.org/docs/2.4/rewrite/flags.html#flag_nc)
				- [NE|noescape](https://httpd.apache.org/docs/2.4/rewrite/flags.html#flag_ne)
				- [NS|nosubreq](https://httpd.apache.org/docs/2.4/rewrite/flags.html#flag_ns)
				- [P|proxy](https://httpd.apache.org/docs/2.4/rewrite/flags.html#flag_p)
				- [PT|passthrough](https://httpd.apache.org/docs/2.4/rewrite/flags.html#flag_pt)
				- [QSA|qsappend](https://httpd.apache.org/docs/2.4/rewrite/flags.html#flag_qsa)
				- [QSD|qsdiscard](https://httpd.apache.org/docs/2.4/rewrite/flags.html#flag_qsd)
				- [QSL|qslast](https://httpd.apache.org/docs/2.4/rewrite/flags.html#flag_qsl)
				- [R|redirect](https://httpd.apache.org/docs/2.4/rewrite/flags.html#flag_r)
				- [S|skip](https://httpd.apache.org/docs/2.4/rewrite/flags.html#flag_s)
				- [T|type](https://httpd.apache.org/docs/2.4/rewrite/flags.html#flag_t)
- Redirecting and Remapping with mod_rewrite
- [Converting Apache Rewrite Rules to NGINX Rewrite Rules](https://www.nginx.com/blog/converting-apache-to-nginx-rewrite-rules/)