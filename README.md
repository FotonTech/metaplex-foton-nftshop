# Install Solana CLI from https://docs.solana.com/cli/install-solana-cli-tools

# Set Devnet as current network
> solana config set --url https://api.devnet.solana.com

# Generate a local wallet
> solana-keygen new --outfile ~/.config/solana/devnet.json
## This is your wallet address
pubkey: ByYmxY3J9rS7QWq47K5nvpjA3zta4xJtwhi6gUVja17G
## This is your secrete phrase
life slim sustain junior decorate onion coil outdoor topple guilt young lemon

# Set keypair
> solana config set --keypair ~/.config/solana/devnet.json

# Put 1 SOL on your wallet
> solana airdrop 1

## In the root of this repo (generally "/metaplex-foton-nftshop")
## Example assets is where your assets (PNG and JSON) are
## Make sure that the fields "image" and "file.uri" from the json are links that points to online images
> ts-node js/packages/cli/src/candy-machine-cli.ts upload js/packages/cli/example-assets --env devnet --keypair ~/.config/solana/devnet.json
## This command is creating the Candy Machine, which is a NFT Generator. The settings and NFT metadata are located on ".cache/devnet-temp.json"


## Initialize a Candy Machine with
#### Price: 0 (Free)
> ts-node js/packages/cli/src/candy-machine-cli.ts create_candy_machine --env devnet --keypair ~/.config/solana/devnet.json --price 0


## Update the settings of the Candy Machine
#### Price: 1 (update the price to 1) (just optional, to show thats possible to edit it)
#### Start date: 26 Sep 2021 00:12:00 GM (Mints start at this date) (mandatory)
ts-node js/packages/cli/src/candy-machine-cli.ts update_candy_machine --keypair ~/.config/solana/devnet.json --price 1 --date "26 Sep 2021 00:12:00 GMT"

## Get the variables from ".cache/devnet-temp.json"
## Update on the Next.js .env variables (on https://vercel.com/fotontech/nftshop-foton/settings/environment-variables) as follow:
      #NEXT_PUBLIC_TREASURY_ADDRESS=<authority>
      #NEXT_PUBLIC_CANDY_MACHINE_CONFIG=<program.config>
      #NEXT_PUBLIC_CANDY_START_DATE=<startDate>
      #NEXT_PUBLIC_SOLANA_RPC_HOST=<rpc from the network that you're using (devnet (https://explorer-api.devnet.solana.com) in this example, find another one on Google)>
      #NEXT_PUBLIC_SOLANA_NETWORK=<devnet,testnet,mainnet-beta>
      #NEXT_PUBLIC_CANDY_MACHINE_ID=<candyMachineAddress>
