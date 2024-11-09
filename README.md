def backtest(data, model):
      # Assume initinitiaAssume initsignalitnitiaAssume initimme initnnitiaAsAssume initimmme initnnnitiainitnnnitiinitnnnitiainitnnnitiialial capital of $100,000
          capital = 100000
              position = 0  # Current position (1 = long, -1 = short, 0 = no position)
                  trade_log = []

                      for i in range(len(data)):
                              # Predict trading signal (1 = Buy, -1 = Sell)
                                      signal = model.predict([data[features].iloc[i]])[0]

                                              # Buy signalsignal
                                                      if signal == 1 and position == 0:
                                                                  position = capital / data['Close'].iloc[i]
                                                                              capital = 0
                                                                                          trade_log.append(('Buy', data.index[i], data['Close'].iloc[i]))

                                                                                                  # Sell signal
                                                                                                          elif signal == -1 and position > 0:
                                                                                                                      capital = position * data['Close'].iloc[i]
                                                                                                                                  position = 0
                                                                                                                                              trade_log.append(('Sell', data.index[i], data['Close'].iloc[i]))

                                                                                                                                                  # If we still have position left at the end, sell at the last closing price
                                                                                                                                                      if position > 0:
                                                                                                                                                              capital = position * data['Close'].iloc[-1]
                                                                                                                                                                      trade_log.append(('Sell', data.index[-1], data['Close'].iloc[-1]))

                                                                                                                                                                          # Return the final capital
                                                                                                                                                                              return capital, trade_log

                                                                                                                                                                              final_capital, trades = backtest(data, model)
                                                                                                                                                                              print(f"Final Capital: ${final_capital:,.2f}")
                                                                                                                                                                              for trade in trades:
                                                                                                                                                                                  print(f"{trade[0]} at {trade[1]} for ${trade[2]:,.2f}")
