#this line has been added:-)

# FF-cli

FF stands for two expressions. the first one is a noun, "Facila File Explorer", which is the name of this software. the second one is a dummy verb, "to Facilifind" which refers to the action of retrieving files using this method. Facilifinding is NOT like search and is NOT like traditional file exploring. It is somehow in between!

## Repository (Repo)

A repository or a repo is basically a directory which supposed to use as Facila storage. It has its own special structure as below.

### Repo File Structure

Path|Content
---|---
`[repo]\`|other DIRs (new files can be copied directly here)
`[repo]\.db\`|database file(s)
`[repo]\.conf\`|config file(s)
`[repo]\.strg\`|here is where files will be stored
`[repo]\.mods\`|modules will be stored here if there were any
`[repo]\*.ff_`|ff_file that introduce a new file to Facila

---

## Commands

As a cli tool Facila should be used using some commands as below.

### General Commands

Action|command
---|---
help|`ff help`
make a repo|`ff init`
show status|`ff status`
evaluate all ff_files|`ff eval -a`
evaluate a ff_file|`ff eval [id]`
update db|`ff update`
add a file|`ff add [source]`
add a file|`ff update`
remove a file|`ff rm [id]`
export a file|`ff save [id] [path]`
revise ff_data of a file|`ff rvz [id]`

### Facilifinding Commands Structure

1. `ff`

    This command reveals a brief overview about all the files which have been stored in the repo. This overview will contain the number of **fields**, **subjects**, **years**, **people**, **places**, etc. which is mentioned in the metadata of the files.

2. `ff [Sth]`

    `[Sth]` can be anything like a subject, a date, a person's name, etc.

    This command will search the phrase `[Sth]` in all the database and returns all files which has it in their metadata.

3. `ff [Wh]`

    `[Wh]` is referring to **WH question words**, we call them **WH lenses**, which are abbreviated as below.

    WH word|Abbreviation
    ---|:---:
    What|`wt`
    When|`wn`
    Where|`wr`
    Who|`wh`
    How|`hw`
    Which|`wc`

    This command reveals a brief overview of all the files. This overview will contain all the values of all the properties of that **WH Lense**.

4. `ff [Wh] [Sth]`

    This command will search the phrase `[Sth]` in `[Wh]` part of database and returns all files which has that phrase in the `[Wh]` part of their metadata.

5. `ff [Wh] --[Switch]`

    This command reveals a brief overview of all the files. This overview will contain all the values of the property which is mentioned by `--[Switch]` or `-[S]`.

6. `ff [Wh] --[Switch] [Sth]` or `ff [Wh] -[S] [Sth]`

    This command will search the phrase `[Sth]` in `[Switch]` subset in `[Wh]` part of database and returns all files which has that phrase in the `[Wh]` part of their metadata.

#### WH lenses and their switches

Lense|Abbr|Switches
---|:---:|---
What|`wt`|Field - Subject
When|`wn`|
Where|`wr`|
Who|`wh`|
How|`hw`|
Which|`wc`|

1. **What** or `wt`
2. **When** or `wn`
3. **Where** or `wr`
4. **Who** or `wh`
5. **How** or `hw`
6. **Which** or `wc`
