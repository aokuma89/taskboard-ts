## これは学校の課題で制作したアプリです


## TaskBoard (TypeScript)
Supabase をバックエンドに使用した、シンプルでモダンなタスク管理（かんばんボード）アプリケーションです。

## 🚀 機能
ユーザー認証: Supabase Auth を利用したサインアップ・ログイン機能。

タスク管理: タスクの追加、ステータス更新、削除。

レスポンシブデザイン: Tailwind CSS による、ダークモード基調のモダンな UI。

リアルタイム性: TypeScript による型安全な開発。

## 🛠 使用技術
Frontend: React, TypeScript, Vite

Styling: Tailwind CSS, Lucide React (アイコン)

Backend: Supabase (Auth, Database)

## 📋 セットアップ手順
1. リポジトリをクローン
Bash
git clone https://github.com/aokuma89/taskboard-ts.git
cd taskboard-ts
2. 依存関係のインストール
Bash
npm install
3. 環境変数の設定
プロジェクトのルートディレクトリに .env ファイルを作成し、Supabase のプロジェクト情報を入力してください。

コード スニペット
VITE_SUPABASE_URL=あなたのSUPABASE_URL
VITE_SUPABASE_ANON_KEY=あなたのSUPABASE_ANON_KEY
4. データベースの準備
Supabase の SQL Editor で tasks テーブルを作成してください。

## SQL
create table tasks (
  id uuid default uuid_generate_v4() primary key,
  user_id uuid references auth.users not null,
  title text not null,
  description text,
  status text check (status in ('todo', 'doing', 'done')) default 'todo',
  created_at timestamp with time zone default timezone('utc'::text, now()) not null
);

-- RLS (Row Level Security) の有効化
alter table tasks enable row level security;

-- ユーザーが自分のタスクのみ操作できるポリシー
create policy "Users can manage their own tasks" on tasks
  for all using (auth.uid() = user_id);
## 5. アプリケーションの起動
Bash
npm run dev
