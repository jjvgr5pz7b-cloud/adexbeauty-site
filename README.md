# adexbeauty.com — nowa strona (statyczna)

Strona firmowa Adex Beauty & Care: HTML/CSS/JS bez frameworka, dwie wersje językowe (EN `/`, PL `/pl/`), hostowana na GitHub Pages.

## Struktura
- `site/` — gotowa strona (to jest publikowane). `index.html` (EN), `pl/index.html` (PL), `privacy.html`, `pl/prywatnosc.html`, `assets/`, `robots.txt`, `sitemap.xml`, `404.html`, `CNAME`.
- `build/` — źródła: `prod.py` (buduje `site/` z prototypu `abc-website-prototype.html`), `site.config.json` (dane firmy, e-mail, endpoint formularza, domena), `gen/` (grafiki).
- `.github/workflows/pages.yml` — automatyczne wdrożenie po każdym pushu na `main`. Jeśli `site/assets/hero.mp4` nie jest w repo, workflow pobiera film z CDN.

## Jak zmienić treść
1. Edytuj `build/abc-website-prototype.html` (tekst EN w elemencie, PL w atrybucie `data-pl`) lub `build/site.config.json`.
2. `cd build && python3 prod.py` (wymaga Pillow: `pip install pillow`).
3. Commit + push na `main` → strona aktualizuje się w ~1 min.

Drobne poprawki można też robić bezpośrednio w `site/*.html` — wtedy nie uruchamiaj `prod.py`, bo nadpisze zmiany.

## Konfiguracja (build/site.config.json)
- `form_endpoint` — adres usługi formularza (Formspree: `https://formspree.io/f/xxxxxxxx`). Dopóki jest `FORM_ENDPOINT`, formularz pokazuje prośbę o kontakt mailowy.
- `email`, `phone`, `phone_tel`, `address_html`, `krs`, `nip`, `social`.
- `base_url` + `cname` — domena, na której strona jest publikowana (dziś `new.adexbeauty.com`). Przy przełączeniu na `adexbeauty.com` zmień oba i przebuduj.

## Domena
GitHub Pages → Settings → Pages → Custom domain = wartość z `CNAME`. W DNS (home.pl): rekord `CNAME new → <konto>.github.io`. HTTPS włącza się automatycznie po weryfikacji.
