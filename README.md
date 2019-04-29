# Swarm tools

This repo contains a collection of [Swarm](http://swarm.ethereum.org) tools that are helpful when developing Swarm.

Currently most of them are dependent on our [Swarm Kubernetes environment](https://github.com/ethersphere/swarm-kubernetes).

## Tools

1.  [correlate](#correlate)
2.  [inspect-subs](#inspect-subs)

## correlate

A tool to help correlate: `host`, `bzz addr` and `node id`, until we consolidate `node id`, `enr` and `bzz addr`.

Example usage:
```
correlate --nodes 70 --namespace tony

or

correlate --nodes 70 --namespace tony --deploymentName swarm-private
```

Dependencies:
1. Make sure you have `kubectl proxy` running in the background.

Results in:

```
host              ; bzz addr                                                          ; id
swarm-private-51	;	9659f733e309ffd66fba288f7bc5b3e491743d91f06cca7f560af38246a94d27	;	29e84afaa8ba35029358de9d445db716ae247b1f598fd3e93aaa52166926329f
swarm-private-49	;	0fbe7635ff86d6b43813d54c6f8b585edf8f5cbee9fab2d282be83bff95d6d70	;	7fdf099b6133276ffce86eb286b3381b78394f65c06488ee34ab94fba5d40ba9
swarm-private-10	;	7552a989594412940263476d078d718dceb6d17420c8b02e4e04b6d1cd5f5dd1	;	c26236b1f6b0435dddee94a6d8dca5ec6aa1aef695160fe38a02de3e62f681fc
swarm-private-28	;	cdd22dd8934d366cb4a7ae0d0d5837920e02badf031ded97a9935caff1f87091	;	f62b02cc3efd82988eeee5009088e00d773417e11df6a0f6cd722b949afa6c3c
swarm-private-21	;	9aee2cd6a9e3ea434fb076aaf3e0dc184fb388314a693e13e754d163e9d44d43	;	3d92af51f7ef60687679a9b33749550857b4145f1b79ab1fe0a6e82d7fbf9313
swarm-private- 1	;	b76146a766844eb7ebcdc2be6a477bb3607079e265a54ff15d6e610370ad030e	;	407b9f0fa95d7a0e78dcbb329cc9289d944ca3625c14b7beaea3610be39d9b74
swarm-private-25	;	383e38f1ae9512bbf972cdf426ef758f8ee2d78d347bc7736e73066f5dca03af	;	07cca8c8e15b9ea1c9e18c61c1b8e2c03fd6946b5d95cb3dd2e97ed7c0d3ffaf
...
```

## inspect-subs

A tool which:

1. Reads the output from `stream_getPeerServerSubscriptions` API,
2. Replaces `node id` with `bzz addr`
3. Prints Kademlia hive table for a specific node, alongside its subscriptions.

Example usage:
```
inspect-subs --nodes 30 --namespace fabio --print-node 0
```

Dependencies:
1. Make sure you have `kubectl proxy` running in the background.


Results in:
```
host                    ;       bzz addr                                                                ;       id
swarm-private- 0	;	210c7d654a6be710c16295d95f9e85c2588c0dba0d668f94d87d54bee498306e	;	cf8d9b88f5dd783740a3447bf82b0fae7258b0a26a52ba781a9f388b3fcef49f

KADEMLIA
---------------------------
=========================================================================
commit hash: 114eb4ae3
Mon Apr 29 09:57:23 UTC 2019 KΛÐΞMLIΛ hive: queen's address: 210c7d654a6be710c16295d95f9e85c2588c0dba0d668f94d87d54bee498306e
population: 41 (55), NeighbourhoodSize: 2, MinBinSize: 2, MaxBinSize: 4
000 22 b8b2 b761 b2ed a55f          | 31 9659 (0) 95d7 (0) 9ce4 (0) 997a (0)
001  7 4d68 4db6 4193 40c7          |  9 5ff5 (0) 4d68 (0) 4db6 (0) 4193 (0)
002  5 07e2 039b 0b30 16a8          |  8 07e2 (0) 039b (0) 0fbe (0) 0a53 (0)
============ DEPTH: 3 ==========================================
003  7 3f28 383e 3229 3109          |  7 383e (0) 3f28 (0) 3229 (0) 3109 (0)
004  0                              |  0
005  0                              |  0
006  0                              |  0
007  0                              |  0
008  0                              |  0
009  0                              |  0
010  0                              |  0
011  0                              |  0
012  0                              |  0
013  0                              |  0
014  0                              |  0
015  0                              |  0
=========================================================================
Subscriptions
----------------------------
039b : 2h, 2l
07e2 : 2l, 2h
0b30 : 2l, 2h
1073 : 2h, 2l
16a8 : 2h, 2l
3109 : gl, 5h, al, bl, dh, el, 3l, 8l, fh, 7h, ch, eh, fl, 4h, 5l, 9l, ah, gh, 4l, 6h, 7l, cl, dl, 6l, 9h, 3h, 8h, bh
3229 : 7l, fl, 3l, 8h, 9h, dl, 6l, 7h, 8l, cl, 3h, 5h, 6h, bh, ah, el, eh, 4l, 4h, 9l, ch, al, fh, gl, 5l, bl, dh, gh
345e : 3l, 6l, 7l, 9l, ah, eh, gh, cl, fh, 8h, 9h, bl, el, 3h, 4l, 5l, dl, dh, fl, 4h, 5h, 7h, al, bh, gl, 6h, 8l, ch
3474 : 5l, 8h, 9h, 6h, bl, fh, 6l, bh, el, gl, dl, dh, 3l, 8l, cl, eh, ch, fl, gh, 3h, 4h, 7l, 9l, 4l, ah, 5h, 7h, al
3639 : 3l, 4h, 5h, cl, fl, 3h, ch, fh, dl, el, 4l, 6l, 7l, 8h, gl, gh, 5l, 9h, 6h, 8l, bh, ah, 7h, 9l, al, bl, dh, eh
383e : 9l, dh, eh, gh, 3l, 5l, 7l, 7h, cl, 4l, 6l, el, 3h, bh, fl, 8h, 9h, ch, dl, gl, 4h, 6h, 8l, ah, 5h, al, bl, fh
3f28 : 6l, 7h, al, el, eh, 3l, 7l, fl, 6h, 8l, ah, bl, bh, 3h, cl, 4h, 9l, 9h, gl, 5l, ch, 5h, dl, 4l, 8h, dh, fh, gh
40c7 : 1h, 1l
4193 : 1l, 1h
4d68 : 1l, 1h
4db6 : 1l, 1h
64e4 : 1l, 1h
7552 : 1h, 1l
7d99 : 1l, 1h
82ba : 0l, 0h
8cbb : 0h, 0l
8e26 : 0l, 0h
997a : 0l, 0h
9aee : 0h, 0l
9b73 : 0h, 0l
9ce4 : 0l, 0h
a55f : 0l, 0h
a8c9 : 0l, 0h
a9a5 : 0l, 0h
ab84 : 0l, 0h
b2ed : 0l, 0h
b761 : 0l, 0h
b8b2 : 0h, 0l
c006 : 0l, 0h
c2a4 : 0l, 0h
cdd2 : 0l, 0h
de24 : 0l, 0h
e4cd : 0h, 0l
e8d7 : 0l, 0h
fdf7 : 0l, 0h
```
