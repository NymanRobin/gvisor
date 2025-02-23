# https://hub.docker.com/r/ollama/ollama
FROM ollama/ollama:0.1.26

ENV PATH=$PATH:/usr/local/nvidia/bin:/bin/nvidia/bin
ENV OLLAMA_ORIGINS=*
ENV OLLAMA_HOST=0.0.0.0:11434

# Pre-install models useful for benchmarking.
# These are huge (total ~120 GiB), but necessary to benchmark
# models of various sizes. They are in their own image file to
# keep the test-only image lighter by comparison.
RUN bash -c '                                  \
    ( ollama serve ) & serverpid="$!";         \
    sleep 5;                                   \
    ollama pull codellama:7b-instruct  &&      \
    ollama pull codellama:34b-instruct &&      \
    ollama pull llama2-chinese:7b-chat &&      \
    ollama pull llama2:13b-chat        &&      \
    ollama pull llama2:70b-chat        &&      \
    ollama pull mistral:7b-instruct    &&      \
    ollama pull mixtral:instruct       &&      \
    ollama pull gemma:2b-instruct      &&      \
    ollama pull gemma:7b-instruct      &&      \
    ollama pull llava:7b-v1.6          &&      \
    ollama pull llava:34b-v1.6         &&      \
    kill "$serverpid" &&                       \
    wait "$serverpid"                          \
'
