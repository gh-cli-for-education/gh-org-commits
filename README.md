
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
  -t --total
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

### total

The output json is simplified as an array in which only the repo lab and the total number of commits is shown:

```json
[
  {
    "name": "aprender-markdown-alejandro-febles-casquero-alu0101013282",
    "total": 7
  },
  {
    "name": "aprender-markdown-alejandro-sanchez-alu0100086393",
    "total": 6
  },
  ...
]
```

## Example

You must create a file with the students names, one per line, and use it as input for the command. An easy way to create it is with the extension `org-teams-names`:

```
✗ gh org-teams-names --org ULL-ESIT-PL-2223 | head -4
adal-diaz-farinya-alu0101112251
adrian-fleitas-de_la_rosa-alu0101024363
adriano-dos_santos-alu0101436784
adrian_grassin-luis-alu0101349480
...
```

Given this team names file:

        ➜  apuntes git:(main) ✗ cat _data/team-names.txt 
        "miguel-rodriguez-caputo-alu0100708974"
        # comments and empty lines are ignored
        #"luis-fernando-fernandez-alu0101232775"
        "maria-Suarez-alu0101232775"
        #"maria-fernanda-fernandez-alu0101232775"

the following command 

```
✗ gh org-teams-names --org ULL-MFP-AET-2223 > /tmp/aet-teams
```

Creates the file `/tmp/aet-teams` with the team names and the command

```
✗ gh org-commits -f /tmp/aet-teams \
             -d '2022-10-27' \
             -l 'aprender-markdown'  \
             -o ULL-MFP-AET-2223 > /tmp/commits-for-aprender-markdown.json
```

Produces warnings for the students that have not created the repository yet:

``` 
gh: Could not resolve to a Repository with the name 'ULL-MFP-AET-2223/aprender-markdown-alumnoudv4-crguezl-parallel'.
gh: Could not resolve to a Repository with the name 'ULL-MFP-AET-2223/aprender-markdown-casiano-rodriguez-leon-alumnoudv4'.
gh: Could not resolve to a Repository with the name 'ULL-MFP-AET-2223/aprender-markdown-luis-manuel-perez-alu0100503791'.
```

and gives a JSON like this one:

```json
[
  {
    "history": [
      {
        "author": {
          "email": "116426203+afeblesc@users.noreply.github.com",
          "name": "afeblesc",
          "user": {
            "login": "afeblesc"
          }
        },
        "authoredDate": "2022-10-30T11:02:27Z",
        "committedDate": "2022-10-30T11:02:27Z",
        "history": {
          "totalCount": 13
        },
        "id": "C_kwDOITJiddoAKGZiNzhmNWY0Mzg1ZGZlYTZlN2Y1MTI0ZmVhMzgxZDNkNzgyNTMyYTY",
        "message": "Update README.md",
        "messageHeadline": "Update README.md",
        "oid": "fb78f5f4385dfea6e7f5124fea381d3d782532a6",
        "pushedDate": "2022-10-30T11:02:28Z"
      },
      ...
    ],
    "total": 7,
    "name": "aprender-markdown-alejandro-febles-casquero-alu0101013282"
  },
  ...
]
```  