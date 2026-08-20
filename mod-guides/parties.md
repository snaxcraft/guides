# Parties -- co-op party for shared quests

**Edition:** Java  
**Version:** 26.2 Paper  
**Last verified:** 2026-08-19  
**Applies to:** `Parties` (`Parties - An advanced parties manager.jar`, AlessioDP **3.2.18**)  
**Host:** Cybrancee **Stone** (4GB) -- see `dev/host-profile.md`

## Summary

**Parties** is the plugin Quests Classic 5.3.2 uses for `share-progress-level: 1`. Together kill/mine and shared dailies (`dailyS*`) only copy progress to **party members who are online**. Personal ladder and personal dailies stay isolated (`share-progress-level: 0`).

Do **not** turn Quests `give-at-login` back on to share. That leaks craft/smelt onto personal quests.

snaxcraft uses one **fixed** party named **`snax`**. Players auto-join it on login if they are not already in a party.

Source: https://alessiodp.com/docs/parties  
Source: https://alessiodp.com/docs/parties/commands  
Source: https://alessiodp.com/docs/parties/permissions  
Source: `server/plugins/Parties/parties.yml`  
Source: `dev/mod-list.md`

## Host boot (Paper 26.2)

Jar **3.2.18** from the author/Spigot download (not Hangar **3.2.14**, which is stale). First start downloads libraries (needs outbound net). Host log **2026-08-17** showed `Enabling Parties v3.2.18` then `Parties v3.2.18 enabled` on Paper 26.2. Author store lists through **26.1**; **26.2 is verified here** for this jar.

Source: `server/logs/latest.log` (host pull 2026-08-17)  
Source: https://alessiodp.com/parties

**LastLoginAPI:** skip. Optional; only for offline party admin. Quests share is online-only.

## snaxcraft config

| Key | Value | Why |
|-----|-------|-----|
| `additional.fixed.enable` | `true` | Needed for `party createfixed` |
| `additional.fixed.default-party.enable` | `true` | Auto-join on login |
| `additional.fixed.default-party.party` | `snax` | One co-op party |
| `general.members.on-player-leave-from-server.kick-from-party` | `false` | Stay in party when offline |
| `general.join-leave-messages` | `false` | No login spam |

Source: `server/plugins/Parties/parties.yml`

Commands: `/party` and `/p` (party chat). `/p` is not claimed in `server/commands.yml`. Default group is **not** given `parties.user.*` (plugin defaults those to OP), so players cannot `/party leave` or create extra parties. They only need `parties.user.join.default` for auto-join.

Source: https://alessiodp.com/docs/parties/permissions  
Source: `server/plugins/Parties/config.yml` (`commands.main-commands`)

Friendly fire protection is **toggleable** (`type: command`). Default is protected until someone runs `/party protection off`. Run `/party protection on` to re-enable. LuckPerms: `parties.user.protection` on `default`; member rank has `party.edit.protection` in `parties.yml`.

## First-time host setup

After `parties.yml` is on the host, with the game server **running**:

```text
party createfixed snax
lp group default permission set parties.user.join.default true
lp group default permission set parties.user.protection true
party reload
```

`createfixed` is console-usable. If the party already exists, skip that line.

Then **reconnect** (or restart) so already-online players join `snax`. Auto-join runs on login, not mid-session.

Check: console `party info snax` should list the co-op.

Source: https://alessiodp.com/docs/parties/commands

## Quests coupling

Together and `dailyS*` emit `share-progress-level: 1` and do **not** set `use-parties-plugin: false`. Personal quests set both `use-parties-plugin: false` and `share-progress-level: 0`.

Progress does not copy to **offline** party members.

### Catch up after share was broken

Quests has **no set-count** command. Equalize from `/q` (copy the exact name, including the dash). Run as op **in-game**, not console -- shared daily names use an em dash that the console can mangle.

Same current quest, different numbers (Hunt 25 Chickens 5/25 vs 0/25): leave it, or `questadmin finish` the behind player if the ahead player already completed it. Do not YAML-edit live player files while they are online.

Different Together tip (A on Kill 500 Zombies, B still on Kill 100):

```text
questadmin quit <behind> Together - Kill 100 Zombies
questadmin give <behind> Together - Kill 500 Zombies
```

Use the **exact** names from the ahead player's `/q`. `finish` also works but pays QP/items/next-step rewards to the behind player -- only do that if you want them to get those rewards.

Shared daily one person already finished:

```text
questadmin finish <behind> Shared Daily — Hunt 25 Chickens
```

Then both reconnect and confirm `party info snax` lists both names, or the split happens again.

Source: `server/plugins/Quests/storage/quests.yml`  
Source: https://pikamug.gitbook.io/quests/setup/commands-and-permissions.md  
Source: [`quests-classic.md`](quests-classic.md)

## Troubleshooting

| Symptom | Check |
|---------|--------|
| Shared quest still personal | Both players in `snax` (`party info snax`); both **online** holding the same quest |
| Auto-join skipped | LuckPerms `parties.user.join.default` on `default`; party `snax` exists; player not already in another party |
| `createfixed` unknown | `additional.fixed.enable: true` then `party reload` |
| Personal Bake Bread leaked | `give-at-login` must stay **false**; do not "fix" share that way |

## See also

- [`quests-classic.md`](quests-classic.md) -- share options and `give-at-login`  
- [`guide/snaxcraft-quests.md`](../guide/snaxcraft-quests.md) -- Together catalog  
- [`guide/snaxcraft-dailies.md`](../guide/snaxcraft-dailies.md) -- shared dailies  
- Author: https://alessiodp.com/docs/parties
