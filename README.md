
# gh extension for GitHub CLI gh org-commits

## Installation

```
gh extension install gh-cli-for-education/gh-org-commits
```

## Usage

```
✗ gh org-commits --help
USAGE
  gh-org-commits [options]
Available options:
  -o --ORG <GitHub Organization>
  -l --lab <gh classroom assignment>
  -d --day <yyyy-mm-dd>
  -f --file <file with students>
  -b --begin <HH:MM:SS>
  -e --end <HH:MM:SS>
  -z --timezone [timezone]
Example:
  gh org-commits -o "my-org" -l "lab-1" -d "2020-09-01" -f "students.txt" -b "00:00:00" -e "23:59:59" -z "Z"
```

## Example


      ✗ gh org-commits -f _data/team-names.txt -d '2022-10-27' -l 'aprender-markdown' | jq '[ .[] | { name: .name, total: .total }]'
        [
          {
            "name": "aprender-markdown-miguel-rodriguez-caputo-alu0100708974",
            "total": 6
          },
          {
            "name": "aprender-markdown-maria-Suarez-alu0101232775",
            "total": 4
          }
        ]

        ➜  apuntes git:(main) ✗ cat _data/team-names.txt 
        "miguel-rodriguez-caputo-alu0100708974"
        # comments and empty lines are ignored
        #"luis-fernando-fernandez-alu0101232775"
        "maria-Suarez-alu0101232775"
        #"maria-fernanda-fernandez-alu0101232775"

