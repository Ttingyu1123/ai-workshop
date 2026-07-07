# Verification Checklist

Run these checks before considering a content or page change done.

## Structural Checks

- Every HTML file ends with `</html>`.
- Every page has GA4 `G-L05KFZJS9L`.
- Header links are unchanged except the active section class.
- Hero badge matches the page's section and reading order.
- Bottom `nav-links` follow the reading chain.
- New pages are added to `index.html` and `sitemap.xml`.

## Prompt Checks

- If a page has `.copy-btn`, it also has `function copyPrompt`.
- If a page has no prompt copy buttons, it should not need `copyPrompt`.
- Prompt examples must not include identifiable patient data.

## Link And Asset Checks

- Check local `href` and `src` references point to existing files.
- Check image files exist for every `img src`.
- External links to tools should be current and preferably official.
- For `404.html`, absolute `/ai-workshop/` paths are expected.

## Content Checks

- Pages with pricing, quotas, plan names, model names, or availability include an update note.
- Numbers are sourced or phrased conservatively.
- Medical claims include safety caveats and verification instructions.
- Each lesson page includes a practical "現在就做" task before bottom navigation.

## Useful PowerShell Snippets

```powershell
# Prompt/script consistency
$rows = @()
foreach ($p in Get-ChildItem -Filter *.html) {
  $text = Get-Content -Raw -Encoding UTF8 $p.FullName
  $rows += [pscustomobject]@{
    Page = $p.Name
    CopyButtons = ([regex]::Matches($text, 'class="copy-btn"')).Count
    CopyFunction = ([regex]::Matches($text, 'function copyPrompt')).Count
    BoxSuccess = ([regex]::Matches($text, 'class="box-success"')).Count
    GA = ($text -match 'G-L05KFZJS9L')
    EndsHtml = ($text.TrimEnd() -like '*</html>')
  }
}
$rows | Format-Table -AutoSize
```

```powershell
# Local href/src existence
$missing = @()
foreach ($p in Get-ChildItem -Filter *.html) {
  $text = Get-Content -Raw -Encoding UTF8 $p.FullName
  foreach ($m in [regex]::Matches($text, '(?:href|src)="([^"]+)"')) {
    $u = $m.Groups[1].Value
    if ($u -match '^(https?:|mailto:|tel:|#|/ai-workshop/|data:)') { continue }
    $path = ($u -split '#')[0]
    if ($path -and -not (Test-Path -LiteralPath (Join-Path (Get-Location) $path))) {
      $missing += [pscustomobject]@{ Page = $p.Name; Ref = $u }
    }
  }
}
$missing | Format-Table -AutoSize
```
