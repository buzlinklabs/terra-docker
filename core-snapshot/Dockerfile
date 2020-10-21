ARG CHAIN_ID
ARG CORE_TAG=${CHAIN_ID}

FROM buzlinklabs/terra-core:${CORE_TAG}

ARG CHAIN_ID
ARG ENV_MONIKER
ARG ENV_MIN_GAS_PRICES
ARG ENV_SEEDS

ENV MONIKER=${ENV_MONIKER}
ENV MIN_GAS_PRICES=${ENV_MIN_GAS_PRICES}
ENV SEEDS=${ENV_SEEDS}
ENV LCD_CHAIN_ID=${CHAIN_ID}

COPY wait-sync.sh /usr/local/bin/wait-sync.sh

USER root
RUN adduser terra-snapshot --disabled-password --uid 2000
WORKDIR /home/terra-snapshot
USER terra-snapshot

RUN LCD_ENABLE=true && cp /home/terra/genesis.json ~/genesis.json && run-terrad.sh & wait-sync.sh

USER terra
WORKDIR /home/terra

CMD run-terrad.sh