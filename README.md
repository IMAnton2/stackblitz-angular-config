# github-angular-config

[Edit on StackBlitz ⚡️](https://stackblitz.com/edit/github-angular-config)

```mermaid
%%{init: {"flowchart": {"defaultRenderer": "elk", "curve": "orthogonal"}} }%%
flowchart TD

A([Should we send a notification?])

A --> B{Thread message && User subscribed?}
B -->|Yes| C{Channel muted?}
B -->|No| C

C -->|Yes| NO1([NO])
C -->|No| D{User in Do Not Disturb?}

D -->|Yes| E{Do Not Disturb Override?}
D -->|No| F{@channel/@everyone/@here message?}

E -->|Yes| F
E -->|No| NO1

F -->|Yes| G{@channel mentions suppressed?}
F -->|No| H

G -->|Yes| NO1
G -->|No| H

H{Channel notification pref is "Nothing"?}
H -->|Yes| I{Thread message && User subscribed?}
H -->|No| J

I -->|Yes| J
I -->|No| NO1

J{User's channel notification pref (device)?}

J -->|Nothing| NO1
J -->|Everything| YES1([YES])

J -->|Mentions| M{DM?}
M -->|Yes| YES1
M -->|No| N{@mention?}
N -->|Yes| YES1
N -->|No| O{Comment on file owned by user?}
O -->|Yes| YES1
O -->|No| NO1

J -->|Default| P{User presence active?}

P -->|Yes| Q{Thread message?}
P -->|No| R

Q -->|Yes| S{User subscribed?}
Q -->|No| R

S -->|Yes| R
S -->|No| NO1

R{Global notification pref?}

R -->|All| GA{Thread message?}
GA -->|Yes| GB{User subscribed?}
GA -->|No| YES1
GB -->|Yes| YES1
GB -->|No| NO1

R -->|Mentions| M1{Thread message?}
M1 -->|Yes| M2{User subscribed?}
M1 -->|No| M3{DM?}
M2 -->|Yes| M3
M2 -->|No| NO1
M3 -->|Yes| YES1
M3 -->|No| M4{@mention?}
M4 -->|Yes| YES1
M4 -->|No| M5{Highlight word?}
M5 -->|Yes| YES1
M5 -->|No| NO1

R -->|"DMs (mobile)"| DM1{DM?}
DM1 -->|Yes| YES1
DM1 -->|No| NO1

R -->|"Highlight Words (mobile)"| HL1{Highlight word?}
HL1 -->|Yes| YES1
HL1 -->|No| NO1

R -->|Never| NO1

YES1 --> MB{Mobile?}
MB -->|Yes| MB2{Past mobile push timing threshold?}
MB -->|No| YES1
MB2 -->|Yes| YES1
MB2 -->|No| YES1

style NO1 fill:#ffdddd,stroke:#ff0000,stroke-width:2
style YES1 fill:#ddffdd,stroke:#009900,stroke-width:2
```