This page documents the [`argument-based-command-permissions`](https://github.com/lucko/LuckPerms/wiki/Configuration#argument-based-command-permissions) configuration option.

When this option is enabled, LuckPerms will run extra permission checks when a player tries to modify or view permission data.

These permissions allow for finer control over what changes a player is able to do, including preventing them from granting specific groups, or making changes in certain contexts.

The extra checks can be broken down into 3 sections.

### Contents

* [**Checks when a player modifies/views themselves or other users**]()
* [- Modify self]()
* [- Modify another player]()
* [- View self]()
* [- View another player]()
* [**Checks when a player modifies/views a group**]()
* [- Modify a group]()
* [- View a group]()
* [**Checks when a player makes changes in a specific context**]()
* [- Change in the global context]()
* [- Change in a specific set of contexts]()
* [**Checks when a player makes changes with a set of specific arguments**]()

## Checks when a player modifies/views themselves or other users

### Modify self

When a player tries to use a command to modify themselves, LuckPerms will first check for `[base command permission].modify.self`. If this returns true, the action is will be allowed. If it returns false, the action will not be allowed.

If the player does not have a value set for the check (in other words, it's undefined), LuckPerms will then check for `luckperms.modify.user.self` to obtain a result. If neither checks return true, the action is not allowed.

#### Example
For example, if I run `/lp user Luck clear`, LuckPerms will check for the following permissions in this order.

* `luckperms.user.clear`
* `luckperms.user.clear.modify.self` (if this check returns true, the next permission will not be checked)
* `luckperms.modify.user.self`

If any of the checks return false, the action will not be allowed.

### Modify another player

When a player tries to use a command to modify another user, LuckPerms will first check for `[base command permission].modify.others`. If this returns true, the action is will be allowed. If it returns false, the action will not be allowed.

If the player does not have a value set for the check (in other words, it's undefined), LuckPerms will then check for `luckperms.modify.user.others` to obtain a result. If neither checks return true, the action is not allowed.

#### Example
For example, if I run `/lp user Notch clear`, LuckPerms will check for the following permissions in this order.

* `luckperms.user.clear`
* `luckperms.user.clear.modify.others` (if this check returns true/false, the next permission will not be checked)
* `luckperms.modify.user.others`

If any of the checks return false, the action will not be allowed.

### View self

When a player tries to use a command to view data about themselves, LuckPerms will first check for `[base command permission].view.self`. If this returns true, the action is will be allowed. If it returns false, the action will not be allowed.

If the player does not have a value set for the check (in other words, it's undefined), LuckPerms will then check for `luckperms.view.user.self` to obtain a result. If neither checks return true, the action is not allowed.

#### Example
For example, if I run `/lp user Luck permission info`, LuckPerms will check for the following permissions in this order.

* `luckperms.user.permission.info`
* `luckperms.user.permission.info.view.self` (if this check returns true/false, the next permission will not be checked)
* `luckperms.view.user.self`

If any of the checks return false, the action will not be allowed.

### View another player

When a player tries to use a command to view data about another user, LuckPerms will first check for `[base command permission].view.others`. If this returns true, the action is will be allowed. If it returns false, the action will not be allowed.

If the player does not have a value set for the check (in other words, it's undefined), LuckPerms will then check for `luckperms.view.user.others` to obtain a result. If neither checks return true, the action is not allowed.

#### Example
For example, if I run `/lp user Notch permission info`, LuckPerms will check for the following permissions in this order.

* `luckperms.user.permission.info`
* `luckperms.user.permission.info.view.others` (if this check returns true/false, the next permission will not be checked)
* `luckperms.view.user.others`

If any of the checks return false, the action will not be allowed.

## Checks when a player modifies/views a group

### Modify a group

When a player tries to use a command to modify a group, LuckPerms will first check for `[base command permission].modify.[group name]`. If this returns true, the action is will be allowed. If it returns false, the action will not be allowed.

If the player does not have a value set for the check (in other words, it's undefined), LuckPerms will then check for `luckperms.modify.group.[group name]` to obtain a result. If neither checks return true, the action is not allowed.

#### Example
For example, if I run `/lp group admin clear`, LuckPerms will check for the following permissions in this order.

* `luckperms.group.clear`
* `luckperms.group.clear.modify.admin` (if this check returns true/false, the next permission will not be checked)
* `luckperms.modify.group.admin`

If any of the checks return false, the action will not be allowed.

### View a group

When a player tries to use a command to view data about a group, LuckPerms will first check for `[base command permission].view.[group name]`. If this returns true, the action is will be allowed. If it returns false, the action will not be allowed.

If the player does not have a value set for the check (in other words, it's undefined), LuckPerms will then check for `luckperms.view.group.[group name]` to obtain a result. If neither checks return true, the action is not allowed.

#### Example
For example, if I run `/lp group admin permission info`, LuckPerms will check for the following permissions in this order.

* `luckperms.group.permission.info`
* `luckperms.group.permission.info.view.admin` (if this check returns true/false, the next permission will not be checked)
* `luckperms.view.group.admin`

If any of the checks return false, the action will not be allowed.

## Checks when a player makes changes in a specific context

When a player tries to use a command to make a change to data, where the data being modified is contextual (can be applied in specific servers/worlds/contexts), LuckPerms will check for extra permissions.

### Change in the global context
If the change is being made in the global context, LuckPerms will first check for `[base command permission].usecontext.global`. If this returns true, the action is will be allowed. If it returns false, the action will not be allowed.

If the player does not have a value set for the check (in other words, it's undefined), LuckPerms will then check for `luckperms.usecontext.global` to obtain a result. If neither checks return true, the action is not allowed.

#### Example
For example, if I run `/lp group admin permission set test.node true`, LuckPerms will check for the following permissions in this order.

* `luckperms.group.permission.set`
* `luckperms.group.permission.set.usecontext.global` (if this check returns true/false, the next permission will not be checked)
* `luckperms.usecontext.global`

If any of the checks return false, the action will not be allowed.

### Change in a specific set of contexts
If the change is not being made in the global context, LuckPerms will check the following for each context being used.

It will first check for `[base command permission].usecontext.[context key].[context value]`. If this returns true, the action is will be allowed. If it returns false, the action will not be allowed.

If the player does not have a value set for the check (in other words, it's undefined), LuckPerms will then check for `luckperms.usecontext.[context key].[context value]` to obtain a result. If neither checks return true, the action is not allowed.

#### Example
For example, if I run `/lp group admin permission set test.node true server=factions world=nether`, LuckPerms will check for the following permissions in this order.

* `luckperms.group.permission.set`
* `luckperms.group.permission.set.usecontext.server.factions` (if this check returns true/false, the next permission will not be checked)
* `luckperms.usecontext.server.factions`
* `luckperms.group.permission.set.usecontext.world.nether` (if this check returns true/false, the next permission will not be checked)
* `luckperms.usecontext.world.nether`

If any of the checks return false, the action will not be allowed.

## Checks when a player makes changes with a set of specific arguments

These checks are made for some commands, and are based upon the arguments passed to the command.

For example, the `parent add` command will check for an extra permission depending on which parent is being added.

If I run `/lp user Luck parent add admin`, among the other permissions being checked for, LuckPerms will also check for `luckperms.user.parent.add.admin`. This allows you to give players access to a certain command, but only using certain arguments.

The arguments which are checked are outlined below.

| Command           | Extra argument checks |
|-------------------|-----------------------|
| permission set    | node                  |
| permission unset  | node                  |
| parent add        | group                 |
| parent set        | group                 |
| parent settrack   | group.track           |
| parent remove     | group                 |
| parent cleartrack | track                 |
| meta set          | key                   |
| meta unset        | key                   |
| promote           | track.next-group      |
| demote            | track.old-group       |