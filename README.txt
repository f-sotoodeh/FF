# FF-cli

## Scenario

There are just a few basic actions

1. __Storing new files__

    There are two different ways to add a new file to the repository:
    - Copying a file directly inside of our Repo directory. If there were a metadata file, `[file_name].ff_`, besides our new file Facila use it as metadata source of the new file. Otherwise, the user will be asked for the metadata file, `[file_name].ff_`. The user can edit the file manually and add more information.
    - Adding a new file using `ff add` command. If there were a metadata file, `[file_name].ff_`, besides our new file FF-cli use it as metadata source of the new file. Otherwise, files will copy in the Repo itself and for each file create a metadata file which should be completed by the user. After that user can add them to the database by running the command `ff update`.

2. __Finding a file__

    It never happens that you look for a file that you do not know anything about it. At least a clue should be in your mind and in fact, it pushes you to look for the file. So, when the user wants to access to a file they know something about it and this is exactly what Facila needs to find the file. So they can easily answer some _Wh questions_ based on what they already know about their intended file. They select the questions to answer using commands. Answer them and Facila will find the file. This action will be called __Facilifinding__ from now.

3. __Modifying the metadata of a file__

    Before modifying the metadata of a file user should find the file then they can copy the metadata to a metadata file by running the command `ff rvz`. Afterward, user can modify the newly created metadata file and run `ff update` to add changes to the database.

4. __Removing a file__

    Just like _Modifying the metadata of a file_, which is mentioned, the user should facilifind and specify their intended file and easily pass it to the remove command.
    `ff rm $([facilifinding commands])`

## Introduction

What Facila really is?

The way we work with storages and explore files is exactly the way we used 100 years ago!
...

**FF** stands for two expressions. the first one is a noun, "Facila File Explorer", which is the name of this software. The second one is a dummy verb, "to Facilifind" which refers to the action of retrieving files using this method. Facilifinding is NOT like search and is NOT like traditional file exploring. It is somehow in between!

## Repository (Repo)

A repository or a repo is basically a directory which supposed to use as Facila storage. It has its own special structure as below.

### Repo File Structure

Path|Content
---|---
`[repo]\`|other DIRs (new files can be copied directly here)
`[repo]\.db\`|database files
`[repo]\.conf\`|config files
`[repo]\.strg\`|here is where files will be stored
`[repo]\.mods\`|modules will be stored here
`[repo]\*.ff_`|ff_file that introduce a new file to Facila

---

## Commands

As a cli tool, Facila should be used using some commands as below.

### General Commands

Action|Command
---|---
help|`ff help`
make a repo|`ff init`
show status|`ff status`
evaluate all ff_files|`ff eval`
evaluate a ff_file|`ff eval [id]`
update db|`ff update`
add a file|`ff add [source]`
add a file|`ff update`
remove a file|`ff rm [id]`
export a file|`ff save [id] [path]`
revise ff_data of a file|`ff rvz [id]`
review metadata of a file|`ff rvl [id]`
get a link to access to file|`ff gl [id]`

### Facilifinding Commands Structure

1. `ff`

    This command reveals a brief overview of all the files which have been stored in the repo. This overview will contain the number of **fields**, **subjects**, **years**, **people**, **places**, etc. which is mentioned in the metadata of the files.

2. `ff gl [Sth]`

    `[Sth]` can be anything like a subject, a date, a person's name, etc.

    This command will search the phrase `[Sth]` in all the database and returns all files which have it in their metadata.

3. `ff -[Wh]`

    `-[Wh]` is referring to **WH question words**, we call them **WH lenses**, which are abbreviated as below.

    WH word|Abbreviation
    ---|:---:
    What|`wt`
    When|`wn`
    Where|`wr`
    Who|`wh`
    How|`hw`
    Which|`wc`

    This command reveals a brief overview which will contain all the values of all the properties of that **WH Lens**.

4. `ff gl -[Wh] [Sth]`

    This command will search the phrase `[Sth]` in `[Wh]` part of the database and returns all files which have that phrase in the `[Wh]` part of their metadata.

5. `ff gl -[Wh] ~[Filter]`

    This command reveals a brief overview which will contain all the values of the property which is mentioned by `~[Filter]`.

6. `ff gl -[Wh] ~[Filter] [Sth]`

    This command will search the phrase `[Sth]` in `[Filter]` subset in `[Wh]` part of the database and returns all files which have that phrase in the `[Wh]` part of their metadata.

#### WH lenses and their filters

Every WH Lens has some filters to directly access details. The way that details are defined and work is depending on **Modules** which are active in every lens. Every module adds a set of **filters** to its lens.

_NOTE:_ The lens `hw` is not a dependent lens like other. In fact, it is a helper lens for `wn`, `wr`, `wh` and it defines HOW _a time_, _a place_, or _a person_ relates to our intended file.

1. **What** or `wt`

    `~[Filter]`|Description
    :---:|---
    `f`|field
    `s`|subject
    `k`|keyword

2. **When** or `wn`

    `~[Filter]`|Description
    :---:|---
    `t`|tick
    `c`|To change calendar type, the default is *Gregorian*
    `y`|year
    `m`|month
    `d`|day
    `h`|hour
    `i`|minute
    `s`|second

    _All other calendar types can be defined as modules._

3. **Where** or `wr`

    Module|`~[Filter]`|Description
    ---|:---:|---
    gps|`gps:l`|Coordinates based on latitude and longitude
    adr|`adr:t`|Textual address
    adr|`adr:a`|An area like a country or a city

4. **Who** or `wh`

    Module|`~[Filter]`|Description
    ---|:---:|---
    ||`i`|id
    name|`name:p`|name prefix
    name|`name:f`|first name
    name|`name:m`|middle name
    name|`name:l`|last name
    name|`name:s`|name suffix
    name|`name:k`|nickname
    name|`name:t`|title
    name|`name:n`|full name or part of it
    contact|`contact:e`|email addresses (set)
    contact|`contact:t`|phone numbers (set)
    contact|`contact:a`|addresses (set)
    Social|`social:p`|social network profiles (set)
    job|`...`|...
    roles|`roles:r`|roles can relate a person to others like being _friend of_, _child of_, etc. (set)
    roles|`roles:p`|people are related by a role (set)
    info|`info:b`|birth date
    info|`...`|`...`
    album|`album:a`|avatar or profile photo
    album|`...`|...
    ...|`...`|...

    _Details that are accessible in WHO Lens are dependent on active modules._

5. **How** or `hw`

    `~[Filter]`|Description
    :---:|---
    `a`|accessed
    `m`|modified
    `c`|created
    `r`|related
    `t`|tagged

6. **Which** or `wc`

    Module|`~[Filter]`|Description
    ---|:---:|---
    ||`t`|File type
    ||`e`|File extension
    ||`n`|File name
    movie|`movie:d`|Movie director
    movie|`movie:y`|Production year
    movie|`movie:g`|Movie genre
    movie|`...`|...
    book|`...`|...
    article|`...`|...
    music|`...`|...
    archive|`...`|...
    photo|`...`|...
    doc|`...`|...
    ...|`...`|...

    This lens can use some modules to talk about those properties which are dependent to file types, like _Director_ which belongs to a _Movie_ or _Author_ which belongs to a _Book_.

### Nested Commands

`[Command_1] $([Command_2])`

### Operators

#### General operators

Operator|Description
:---:|---
`~`|using a filter
`$`|run
`:`|using filters of a module
`.`|going through a set

#### Logical operators

Operator|Logic
:---:|---
`?and` or `*`|and
`?or` or `+`|or
`?not` or `!`|not