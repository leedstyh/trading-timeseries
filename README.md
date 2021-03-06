[![Build Status](https://travis-ci.org/evsamsonov/trading-timeseries.svg?branch=master)](https://travis-ci.org/evsamsonov/trading-timeseries)

# Timeseries

Timeseries provides structure for series of trading candles. 

## Installation

```sh
$ go get github.com/evsamsonov/trading-timeseries
```

## Usage


```go
dataset := []struct {
    Time   time.Time
    High   float64
    Low    float64
    Open   float64
    Close  float64
    Volume int64
}{
    {Time: time.Unix(1, 0), High: 1, Low: 2, Open: 3, Close: 4, Volume: 5},
    {Time: time.Unix(2, 0), High: 6, Low: 7, Open: 8, Close: 9, Volume: 10},
}

series := timeseries.New()
for _, item := range dataset {
    candle := timeseries.NewCandle(item.Time)
    candle.Open = item.Open
    candle.Close = item.Close
    candle.High = item.High
    candle.Low = item.Low
    candle.Volume = item.Volume

    err := series.AddCandle(candle)
    if err != nil {
        log.Printf("Failed to add candle: %v\n", err)
    }
}

fmt.Println(series.Candle(0))    // &{1970-01-01 03:00:01 +0300 MSK 1 2 3 4 5}
fmt.Println(series.LastCandle()) // &{1970-01-01 03:00:02 +0300 MSK 6 7 8 9 10}
fmt.Println(series.Length())     // 2
```

TODO 
tickseries
