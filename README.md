# Berrien County MCA public site (org root repo)

Serves at bcmca.github.io and berrienmca.org. Project sites nest underneath:
/protocols (protocol reference), /proposed and /announcements and /about live here.

## One-time: clean PDFs before first push
Drop the clean protocol documents into proposed/pdfs/ with these exact names:

AEMT Specialist group:
- 7-13-specialist-clean.pdf
- 3-3-specialist-clean.pdf
- 4-5-specialist-clean.pdf
- 1-6-specialist-clean.pdf

Epinephrine Infusion group:
- 7-32-epi-infusion-clean.pdf
- 9-23R-epinephrine-clean.pdf
- 8-17-privileges-clean.pdf

Rename freely, but keep proposed/proposed.json "f" fields in sync.

## Deploy
mkdir ~/bcmca-site && cd ~/bcmca-site
unzip ~/Downloads/bcmca_site_build.zip -d .
(copy the clean PDFs into proposed/pdfs/)
git init -b main && git add . && git commit -m "MCA public site"
gh repo create BCMCA/BCMCA.github.io --public --source=. --push
Then: repo Settings > Pages > Deploy from branch, main, / (root).
Verify at bcmca.github.io.

## Custom domain (DNS already configured at Porkbun)
Repo Settings > Pages > Custom domain: www.berrienmca.org > Save.
Wait for DNS check, then tick Enforce HTTPS once available.
All project sites inherit the domain; github.io URLs and printed QRs redirect.

## Publishing routines
Proposed protocols: edit proposed/proposed.json (group: id, heading, status,
posted, comment true/false, docs, optional nested), drop PDFs, push.
Comment deadline renders at posted + 60 days when comment is true.
?comment=GROUPID deep-links a group with its comment panel open.

Announcements: add an entry to announcements/announcements.json
{"d":"YYYY-MM-DD","t":"Title","b":"Body.","a":"optional.pdf"} and push.
Newest sorts first automatically. MCA-speaker content only.

Comment intake: Web3Forms key in proposed/index.html, bound to
comments@berrienmca.org (forwards to AB and Dr. Beyer). Rotate by creating a
new key at web3forms.com for the same address and replacing ACCESS_KEY.

## robots.txt
Disallows /followup/ (Medic 1 program, kept unlisted).
