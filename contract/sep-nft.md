## Preamble

```
CIP: 
Title: NFT
Author: Stellar Development Foundation <@stellar>
Status: Draft
Discussion: TBD
Created: 2023-10-11
Version 0.2.0
```
## Summary

This proposal introduces a standard interface for NFTs on Soroban, ensuring compatibility and interoperability within the Stellar ecosystem, and aligning with the Stellar token interface and SEP0039.

## Motivation

A standardized interface for NFTs on Soroban will facilitate seamless interaction within the Stellar ecosystem, enhancing user experience and developer interaction by providing a consistent framework for NFT creation, transfer, and management.

## Abstract

This proposal introduces a contract interface for NFTs, focusing on ensuring that NFTs on Soroban are compatible with existing contracts and Stellar assets, adhering to the principles and guidelines outlined in SEP0039 and the Stellar token interface, and incorporating practical implementation aspects.

## Specification

```rust
pub trait NFTInterface {
    // Admin interface – privileged functions.
    fn initialize(
        env: Env, 
        admin: Address, 
        name: String, 
        symbol: String, 
        royalty_recipient: Address, 
        royalty_percentage: u32, 
        short_uri: String, 
        detailed_uri: String, 
        long_uri: String
    );

    // Token interface
    fn transfer(env: Env, from: Address, to: Address, token_id: u32);

    fn approve(
        env: Env, 
        owner: Address, 
        approved: Address, 
        token_id: u32
    );

    fn transfer_from(
        env: Env, 
        from: Address, 
        to: Address, 
        token_id: u32
    );

    // Descriptive Interface
    fn get_metadata(env: Env, token_id: u32) -> Metadata;

    fn decimals(env: Env) -> u32;

    fn name(env: Env) -> String;

    fn symbol(env: Env) -> String;

    fn get_royalty_recipient(env: Env) -> Address;

    fn get_royalty_rate(env: Env) -> u32;
}

// Metadata struct to hold NFT metadata, including descriptions and IPFS hashes.
struct Metadata {
    short_description_uri: String,  //\ IPFS hash or URL
    long_description_uri: String,   // IPFS hash or URL
    data_file_uri: String,          // IPFS hash or URL
}
```

### Notes:
- The `initialize` function sets up the NFT with essential information, including royalty details and URIs for metadata.
- The `get_metadata` function retrieves the metadata for a specific NFT, identified by its `token_id`.
- The `Metadata` struct holds relevant information about the NFT, including URIs for descriptions and associated data.
- The `decimals` function should always return `0` for NFTs.
- The `transfer`, `approve`, and `transfer_from` functions facilitate the transfer of NFTs between addresses, with approval mechanisms.
- The `get_royalty_recipient` and `get_royalty_rate` functions provide information about the royalty recipient and rate respectively.

This draft is a starting point and may need further refinement and additional functions to fully cater to the use-cases and requirements of NFTs on Soroban while ensuring compatibility with the Stellar token interface and adherence to SEP0039.
## Changelog

- `v0.1.0` - Initial draft based on CIP-001.
- `v0.2.0` - Revised draft incorporating Soroban token interface and additional metadata methods.

## Implementations

TBD
