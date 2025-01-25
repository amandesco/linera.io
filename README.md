# linera.io
SELECT
  DATE_TRUNC('month', block_date) AS period,
  SUM(tx_fee_usd) AS monthly_gas_spent,
  SUM(SUM(tx_fee_usd)) OVER (ORDER BY DATE_TRUNC('month', block_date)) AS cumulative_gas_spent
FROM gas.fees
WHERE
  tx_sender = {0xc1e153BDa003E9764549BaC71Af0CF5AA0D2E3C6}
GROUP BY
  DATE_TRUNC('month', block_date)
ORDER BY
  1
