## Versions

anchor-cli 1.1.2 · node 22.x · @codama/cli 1.6.3

## TODO 3

Required: `fundraiser`, `vault`. Optional: `contributorAccount`, `contributorAta`, `tokenProgram`, `systemProgram`.

For `contribute`, `contributorAccount` can be derived because its PDA seeds use the fundraiser and contributor addresses, which are already available. `contributorAta` can also be derived from the contributor and mint information, and `tokenProgram` is a known program address.

The `fundraiser` account cannot be derived automatically because its PDA is seeded with:

`["fundraiser", fundraiser.maker]`

Here, `maker` is a field stored inside the fundraiser account itself. The finder would need the fundraiser account to know its maker, but it needs the fundraiser address first. So `fundraiser` has to be provided explicitly.

This differs from `initialize`, where the `maker` account is already available as an instruction input, so the fundraiser PDA can be derived directly.

## Bonus

not attempted

## One thing that surprised me

I expected Codama to derive more of the accounts automatically, but the PDA seed dependencies determine whether an account can actually be resolved. In particular, the `fundraiser` PDA depends on data stored inside the very account being derived, so Codama cannot resolve it from the other instruction inputs.