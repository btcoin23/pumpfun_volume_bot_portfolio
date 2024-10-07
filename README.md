# Pumpfun Volume Bot
This is a Pump.fun volume bot that can increase the volume of a specific Pump.fun token.

## Screenshot

![image](https://github.com/user-attachments/assets/fc57859d-0e89-4cf2-be98-81b22c4ccc5b)

## Main functions (Fast, Low Fee, Effeciency)

- Analyze the specific pumpfun token's details including its `bondingCurve`, `associatedVondingCurve`, `virtualTokenReserve` and `virtualSolReserve`, etc.

- Create new wallets

- Create new Lookuptable

    https://explorer.jito.wtf/bundle/9cf9cc9090964cae053dd8031be6b6811dabd21fd5151cc93cb2ecc2036665c2

- Extend Lookuptable

    https://explorer.jito.wtf/bundle/131f0680d89996bb556763f22979249cd69f1179a0c5649f33fcaf3bb552ef90

- Distribute SOL to sub wallets using LUT, Jito

    https://explorer.jito.wtf/bundle/ce4da11d89d6adc17c2a954146b7ded8c8cef07379c1712ea36dbef52e79318d

- Swap(buy/sell in the same transaction) with 20 wallets

     https://explorer.jito.wtf/bundle/ea93969c37d22f90e20b2977220299c495d469f66a4a96906d4166654c6b2cd2

- Collecting sol to main wallet

    https://explorer.jito.wtf/bundle/a136bee41fae40dd73747059d0604a91018b6416f9831915f9b67db7ae9293f2

## How to run

1. Clone this repository to your local machine:

   ```bash
   git clone https://github.com/btcoin23/pumpfun_volume_bot.git
   ```

2. Navigate to the project directory:

   ```bash
   cd pumpfun_vbot
   ```

3. Install the project dependencies:

   ```bash
   npx yarn 
   ```
4. Create a `.env` file in the project root directory and add your wallet's   secret key, RPC URL, and other necessary configuration.

`.env` file
   ```bash
    RPC_URL=
    PRIVATE_KEY=
   ```

5. Edit the `./src/config.ts` file to configure the bot's settings.
Here, plz set the Pumpfun token's `CA`, `JitoTipAmount` and the `DistributeAmount` of SOL to distribute to each sub-wallet (in case of your wallet funds are 0).

`config.ts` file:
   ```bash
    export const DistributeAmount = 0.01 * LAMPORTS_PER_SOL; // 0.01 SOL

    export const JitoTipAmount = 0.0001 * LAMPORTS_PER_SOL; // 0.0001 SOL
    export const CA = '6YGUi1TCwEMLqSmFfPjT9dVp7RWGVye17kqvaqhwpump';
   ```

6. Edit the `wallet.json` file to edit sub-wallets. At first, the bot uses wallets from this file.
Then you can edit the `index.ts` file to create new wallets, distribute & collect SOL.

`index.ts` file:
   ```bash
    (async () => {
        const pumpBot = new PumpfunVbot(CA);
        await pumpBot.getPumpData();
        // pumpBot.createWallets(); // Optional for creating new 20 wallets
        pumpBot.loadWallets();
        await pumpBot.createLUT();
        await pumpBot.extendLUT();
        await pumpBot.loadLUT();
        // await pumpBot.distributeSOL(); // Optional for distributing sol to 20 wallets
        while(true){
            await pumpBot.swap();
            await sleepTime(3000);
        }
        // await pumpBot.collectSOL(); // Optional for collecting sol to main wallet
    })();
   ```

7. Start the bot

   ```bash
   npm start
   ```

## Author
- [Github](https://github.com/btcoin23)
- [Telegram](https://t.me/BTC0in23)
