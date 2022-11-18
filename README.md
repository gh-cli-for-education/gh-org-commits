
# gh extension for GitHub CLI gh org-commits

## Installation

```
gh extension install gh-cli-for-education/gh-org-commits
```

## Usage

```
➜  gh-org-commits git:(main) gh org-commits --help
USAGE
  gh org-commits [-o|--ORG <ORG>] [-l|--lab <gh classroom assignment>] [-d|--day <year-month-day>] [-f|--file <students file>] [-b|--begin <HH:MM:SS>] [-e|--end <HH:MM:SS>]
```

## Example

```
✗ gh org-commits -f _data/team-names.txt -d '2022-10-27' -l 'aprender-markdown' | jq '[ .[] | { name: .name, total: .total }]'
[
  {
    "name": "aprender-markdown-gerardo-rodriguez-caputo-alu0100708974",
    "total": 6
  },
  {
    "name": "aprender-markdown-Laura_Lourdes-Suarez-alu0101232775",
    "total": 4
  }
]
```