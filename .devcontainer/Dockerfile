# Pythonのベースイメージを指定
FROM python:3.11.2-slim

# Poetryをインストール
ENV POETRY_VERSION=1.4.0
RUN pip install --no-cache-dir "poetry==$POETRY_VERSION"

# 作業ディレクトリを設定
WORKDIR /workspaces/fastapi-project

# poetryの設定: 仮想環境を作成しないように設定
RUN poetry config virtualenvs.create false

# vscode ユーザーの追加
RUN useradd -m vscode && \
    chown -R vscode:vscode /workspaces/fastapi-project

# Poetry関係のファイルをコピー
COPY pyproject.toml /workspaces/fastapi-project/
COPY poetry.lock /workspaces/fastapi-project/

# 依存関係をインストール
RUN poetry install --no-dev

# Python パスの設定
ENV PYTHONPATH=/workspaces/fastapi-project

# ユーザーを切り替える
USER vscode

# サーバー起動
# uvicorn fastapi_project.main:app --host 0.0.0.0 --port 8000
ENTRYPOINT ["uvicorn", "fastapi_project.main:app", "--host", "0.0.0.0", "--port", "8000"]
