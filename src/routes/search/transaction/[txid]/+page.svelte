<script lang="ts">
  export let data: {
    transaction: {
      'Transaction ID': string;
      Inputs: any[];
      Outputs: any[];
      Amount: number;
      Timestamp: string | null;
      'Block Hash': string;
    };
  };

  let error: string | null = null;
  if (!data.transaction) {
    error = 'Failed to load transaction data';
  }
</script>

<body class="static-gradient flex flex-col justify-center">
  <main class="flex-grow flex flex-col items-center justify-center space-y-4 px-4">
    <div class="text-center">
      <h1 class="text-4xl font-bold">Transaction Details</h1>
    </div>
    <section class="glass2 p-8 rounded-xl shadow-lg w-full max-w-6xl">
      {#if data.transaction}
        <div class="space-y-4 text-left">
          <div>
            <span class="font-bold">Transaction ID:</span> <span>{data.transaction['Transaction ID']}</span>
          </div>
          <div>
            <span class="font-bold">Inputs:</span>
            <ul class=" list-inside ml-4">
              {#each data.transaction.Inputs as input, index}
                <li>
                  <div class="ml-4">
                    <div><span class="font-bold">Coinbase:</span> <span>{input.coinbase}</span></div>
                    <div><span class="font-bold">TxID:</span> <span>{input.txid}</span></div>
                    <div><span class="font-bold">Vout:</span> <span>{input.vout}</span></div>
                    <div><span class="font-bold">ScriptSig ASM:</span> <span>{input.scriptSig.asm}</span></div>
                    <div><span class="font-bold">ScriptSig HEX:</span> <span>{input.scriptSig.hex}</span></div>
                    <div><span class="font-bold">Sequence:</span> <span>{input.sequence}</span></div>
                  </div>
                </li>
              {/each}
            </ul>
          </div>
          <div>
            <span class="font-bold">Outputs:</span>
            <ul class="list-inside ml-4">
              {#each data.transaction.Outputs as output, index}
                <li>
                  <div class="ml-4">
                    <div><span class="font-bold">Value:</span> <span>{output.value}</span></div>
                    <div><span class="font-bold">N:</span> <span>{output.n}</span></div>
                    <div><span class="font-bold">ScriptPubKey ASM:</span> <span>{output.scriptPubKey.asm}</span></div>
                    <div><span class="font-bold">ScriptPubKey HEX:</span> <span>{output.scriptPubKey.hex}</span></div>
                    <div><span class="font-bold">ReqSigs:</span> <span>{output.scriptPubKey.reqSigs}</span></div>
                    <div><span class="font-bold">Type:</span> <span>{output.scriptPubKey.type}</span></div>
                    <div><span class="font-bold">Addresses:</span> <span>{output.scriptPubKey.addresses.join(', ')}</span></div>
                  </div>
                </li>
              {/each}
            </ul>
          </div>
          <div>
            <span class="font-bold">Amount:</span> <span>{data.transaction.Amount}</span>
          </div>
          <div>
            <span class="font-bold">Timestamp:</span> <span>{data.transaction.Timestamp}</span>
          </div>
          <div>
            <span class="font-bold">Block Hash:</span> <span>{data.transaction['Block Hash']}</span>
          </div>
        </div>
      {:else if error}
        <p class="text-red-500">{error}</p>
      {/if}
    </section>
  </main>
</body>
