# CAAZ Eval360 — GitHub and deployment

Static files only. Proposed address: **https://mel.eval360.tech/caaz/**, alongside `/fpc`, `/cic` and `/kdc`.

## 1 · Push to GitHub

Create `windantech/caaz-eval360` on GitHub, then:

```bash
cd ~/caaz-eval360
git remote add origin https://github.com/windantech/caaz-eval360.git
git push -u origin main
```

## 2 · First deployment on the server

If the repository is public:

```bash
cd /home/vantage/domains/eval360.tech/public_html/mel
git clone https://github.com/windantech/caaz-eval360.git caaz
cd caaz
bash scripts/deploy_pull.sh
```

If it is private, clone with `https://USERNAME:TOKEN@github.com/…` instead (token with `repo` scope).

## 3 · Every update

```bash
bash scripts/selftest.sh          # locally — must pass
git add -A && git commit -m "…" && git push
```

On the server:

```bash
cd /home/vantage/domains/eval360.tech/public_html/mel/caaz
bash scripts/deploy_pull.sh
```

## Note

The page is `noindex`. Anything pushed to a public repository is public, including the illustrative
data — which is labelled as such throughout.
