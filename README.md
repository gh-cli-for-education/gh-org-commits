
# gh extension for GitHub CLI gh org-commits

Get the commits of the students for a GitHub Classroom assignment for a specified date range.

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

## Defaults

### ORG

By default the ORG is obtained using the output of command `gh pwd`.
For a better experience:

      set alias pwd to:  !gh config get current-org
      set alias cd to:   !gh config set current-org "$1" 2>/dev/null

### lab

the default `lab` is  set to the output of the command `gh pwd-lab`

      set alias cd-lab to:   !gh config set current-lab "$1" 2>/dev/null  
      set alias pwd-lab to:  !gh config get current-lab

### begin 

00:00:00

### end

23:59:59

### day

Start day. The reported commits will be from this day to today.

### file

_data/team-names.txt


## Example

Given this team names file:

        ➜  apuntes git:(main) ✗ cat _data/team-names.txt 
        "miguel-rodriguez-caputo-alu0100708974"
        # comments and empty lines are ignored
        #"luis-fernando-fernandez-alu0101232775"
        "maria-Suarez-alu0101232775"
        #"maria-fernanda-fernandez-alu0101232775"

the following command `gh org-commits -f _data/team-names.txt -d '2022-10-27' -l 'aprender-markdown' ` 
uses the default value for `org`, `begin` and `end` and so produces a JSON by the uncommented students for the whole day:

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


