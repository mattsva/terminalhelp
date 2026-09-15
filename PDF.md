# PDF tools

## Here we want to delete all the acroform fields out of an pdf with nix-shell
```bash
nix-shell -p python3Packages.pikepdf --run 'python3 -c "
import pikepdf

pdf = pikepdf.Pdf.open(\"pdf.pdf\")
n = 0

for f in pdf.acroform.fields:
    if f.flags & 1:
        f.obj[\"/Ff\"] = int(f.flags) & ~1
        n += 1

print(f\"ReadOnly entfernt bei {n} Feldern\")
pdf.save(\"output.pdf\")
"'
```

## Here we like to get informations about an pdf with nix-shell
```bash
nix-shell -p poppler-utils qpdf exiftool --run '
  pdfinfo ./file.pdf
  echo "===== EXIFTOOL ====="
  exiftool ./file.pdf
  echo "===== QPDF ====="
  qpdf --show-object=trailer ./file.pdf
'
```
