# Motoko Playground Demo
Internet Computer Project Building Workshop

Canister ID: ud6i4-iaaaa-aaaab-qadiq-cai

// importlar

import Nat "mo:base/Nat";
import Nat64 "mo:base/Nat64";
import Cycles "mo:base/ExperimentalCycles";

// canister
// gas fee (cycle)

actor HelloCycles {
  
  // değişkenler

  // let -> immutable
  // var -> mutable

  let limit = 10_000_000;

  // fonksiyonlar (query, update)

  public func wallet_balance() : async Nat {
    // return -> return ...;
    // return -> ...
    Cycles.balance()
    // return Cycles.balance();
  };

  public func wallet_receive() : async { accepted: Nat64} {
    let available = Cycles.available();
    let accepted = Cycles.accept(Nat.min(available, limit));
  { accepted = Nat64.fromNat(accepted) };
  
};

public func transfer(
  receiver: shared() -> async (),
  amount : Nat) : async {refunded: Nat} {
    Cycles.add(amount);
    await receiver();
    {refunded = Cycles.refunded()};
  };
};



