# magic-lookup

```
=ARRAYFORMULA(IF(
  ISBLANK(INDIRECT(
    CONCATENATE("R"; ROW(); "C"; MATCH(REGEXREPLACE(
      INDEX(SPLIT(INDIRECT(ADDRESS(1; COLUMN(); 1)); ":"); 1);
    "^(.+)\[(.+)\]$"; "$1"); $1:$1; 0)); FALSE
  ):INDIRECT(
    CONCAT("R1000000C"; MATCH(REGEXREPLACE(
      INDEX(SPLIT(INDIRECT(ADDRESS(1; COLUMN(); 1)); ":"); 1);
      "^(.+)\[(.+)\]$"; "$1"
    ); $1:$1; 0)); FALSE
  )); ""; VLOOKUP(
    INDIRECT(
      CONCATENATE("R"; ROW(); "C"; MATCH(REGEXREPLACE(
        INDEX(SPLIT(INDIRECT(ADDRESS(1; COLUMN(); 1)); ":"); 1);
        "^(.+)\[(.+)\]$"; "$1"
      ); $1:$1; 0)); FALSE
    ):INDIRECT(
      CONCAT("R1000000C"; MATCH(REGEXREPLACE(
        INDEX(SPLIT(INDIRECT(ADDRESS(1; COLUMN(); 1)); ":"); 1);
        "^(.+)\[(.+)\]$"; "$1"
      ); $1:$1; 0)); FALSE
    );
    INDIRECT(CONCATENATE("'"; REGEXREPLACE(
      INDEX(SPLIT(INDIRECT(ADDRESS(1; COLUMN(); 1)); ":"); 1);
      "^(.+)\[(.+)\]$"; "$2"
    ); "'!$A:$FFF"));
    MATCH(
      REGEXEXTRACT(INDIRECT(ADDRESS(1; COLUMN(); 1)); ":(.+)");
      INDIRECT(CONCATENATE("'"; REGEXREPLACE(
        INDEX(SPLIT(INDIRECT(ADDRESS(1; COLUMN(); 1)); ":"); 1);
        "^(.+)\[(.+)\]$"; "$2"
      ); "'!$1:$1")); 0
    ); FALSE
  )
))
```
