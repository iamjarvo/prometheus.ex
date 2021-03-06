# Prometheus.ex
[![Build Status](https://travis-ci.org/deadtrickster/prometheus.ex.svg?branch=master)](https://travis-ci.org/deadtrickster/prometheus.ex)
[![Hex.pm](https://img.shields.io/hexpm/dt/prometheus_ex.svg?maxAge=2592000)](https://hex.pm/packages/prometheus_ex)
[![Coverage Status](https://coveralls.io/repos/github/deadtrickster/prometheus.ex/badge.svg?branch=master)](https://coveralls.io/github/deadtrickster/prometheus.ex?branch=master)
[![Hex.pm](https://img.shields.io/hexpm/v/prometheus_ex.svg?maxAge=2592000)](https://hex.pm/packages/prometheus_ex)
[![Documentation](https://img.shields.io/badge/documentation-on%20hexdocs-green.svg)](https://hexdocs.pm/prometheus_ex/)

Elixir [Prometheus.io](https://prometheus.io) client based on [Prometheus.erl](https://github.com/deadtrickster/prometheus.erl).

![@skosch dashboard](http://aldusleaf.org/content/images/2016/09/grafana.jpg)

Dashboard from [Monitoring Elixir apps in 2016: Prometheus and Grafana](http://aldusleaf.org/monitoring-elixir-apps-in-2016-prometheus-and-grafana/) by [**@skosch**](https://github.com/skosch).

## Example

```elixir
defmodule ExampleInstrumenter do
  use Prometheus.Metric

  def setup do    
    Histogram.new([name: :http_request_duration_milliseconds,
                   labels: [:method],
                   buckets: [100, 300, 500, 750, 1000],
                   help: "Http Request execution time"])
  end

  def instrument(%{time: time, method: method}) do
    Histogram.observe([name: :http_request_duration_milliseconds, labels: [method]], time)
  end
end
```

## Integrations / Collectors / Instrumenters
 - [Ecto collector](https://github.com/deadtrickster/prometheus-ecto)
 - [Plugs Instrumenter/Exporter](https://github.com/deadtrickster/prometheus-plugs)
 - [Elli middleware](https://github.com/elli-lib/elli_prometheus)
 - [Fuse plugin](https://github.com/jlouis/fuse#fuse_stats_prometheus)
 - [Phoenix instrumenter](https://github.com/deadtrickster/prometheus-phoenix)
 - [Process Info Collector](https://github.com/deadtrickster/prometheus_process_collector.erl)
 - [RabbitMQ Exporter](https://github.com/deadtrickster/prometheus_rabbitmq_exporter)

## Installation

[Available in Hex](https://hex.pm/packages/prometheus_ex), the package can be installed as:

  1. Add `prometheus_ex` to your list of dependencies in `mix.exs`:

    ```elixir
    def deps do
      [{:prometheus_ex, "~> 1.0.0"}]
    end
    ```

  2. Ensure `prometheus_ex` is started before your application:

    ```elixir
    def application do
      [applications: [:prometheus_ex]]
    end
    ```
