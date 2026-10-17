# Katkı Rehberi

Bu repo **GitHub Flow** ile yönetilir: `main` her zaman çalışır durumdadır, her değişiklik kısa ömürlü bir
branch'te yapılır ve pull request ile `main`'e girer.

## Akış

1. **Issue:** Her iş bir issue ile başlar. Issue'su olmayan branch açılmaz.
2. **Branch:** `main`'den açılır, hedef ömrü en fazla 2-3 gündür.
3. **Commit:** Küçük ve anlamlı commit'ler; kod ve doküman ayrı commit'lerde.
4. **Pull request:** Şablon doldurulur, açıklamada `Closes #<issue>` yazılır.
5. **Kontroller:** CI yeşil olmalı, "Files changed" üzerinden self-review yapılır.
6. **Merge:** Yalnızca **squash merge**; branch merge sonrası silinir.

`main`'e doğrudan push yapılmaz.

## Branch adı

```
<tip>/<issue-no>-<kisa-aciklama>
```

Küçük harf, kelimeler tire ile ayrılır, Türkçe karakter kullanılmaz.

| Tip | Ne için? | Örnek |
|---|---|---|
| `feat/` | Yeni özellik | `feat/42-slot-uretimi` |
| `fix/` | Hata düzeltme | `fix/61-iptal-saati-kontrolu` |
| `docs/` | Doküman, ADR | `docs/12-adr-domain-secimi` |
| `refactor/` | Davranışı değiştirmeyen iyileştirme | `refactor/73-appointment-handler` |
| `test/` | Yalnızca test | `test/80-slot-eszamanlilik` |
| `chore/` | Bağımlılık, repo ayarı, araç | `chore/5-editorconfig` |
| `ci/` | CI iş akışları | `ci/9-dotnet-workflow` |

## Commit mesajı

[Conventional Commits](https://www.conventionalcommits.org/) biçiminde, **İngilizce**, emir kipinde, en fazla 72 karakter.

```
<tip>(<kapsam>): <kısa açıklama>

<gövde: neden yapıldı, ne değişti (isteğe bağlı)>

Refs: #<issue>
```

| Tip | Sürüm etkisi |
|---|---|
| `feat` | minor (1.2.0) |
| `fix`, `perf` | patch (1.2.1) |
| `feat!` veya `BREAKING CHANGE:` | major (2.0.0) |
| `docs`, `test`, `refactor`, `chore`, `ci`, `build` | sürüm değişmez |

Kapsam servis veya alan adıdır: `catalog`, `patient`, `appointment`, `examination`, `notification`,
`gateway`, `contracts`, `web`, `adr`, `deps`, `ci`.

```
feat(appointment): add slot booking endpoint with idempotency key
fix(appointment): reject patient cancellation after 20:00 on the previous day
```

**PR başlığı da aynı biçimdedir.** Squash merge'de `main`'e girecek commit mesajı PR başlığından oluşur.

## Pull request

- Hedef boyut: 400 satırın altında değişiklik. Büyük işler bağımsız çalışan küçük PR'lara bölünür.
- CI kırmızıysa veya review'da bulgu varsa düzeltme **yeni commit** ile yapılır; paylaşılan geçmiş yeniden yazılmaz.
- Rebase sonrası yalnızca `git push --force-with-lease` kullanılır.

## Güvenlik

Repoya secret, `.env` dosyası veya gerçek kişi verisi girmez. Tüm test verisi sentetiktir.
Güvenlik açıkları için [SECURITY.md](SECURITY.md).
