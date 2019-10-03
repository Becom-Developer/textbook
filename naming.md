# NAME

naming - 命名規則について

# SYNOPSIS

- 基本的な考え方については良書といわれるものが存在するのでそちらを参考にしておく
- 良書 [SEE ALSO](#see-also) の `Perlベストプラクティス`, `リーダブルコード` を参考
- この記事は少人数(3~4人程度)で作業することを想定した命名規則の参考事例とする

# THINK

__プログラミング全般に対しての命名規則の考え方__

- 命名規則の考え方と実際に命名することについては分けて考える
- なんのための命名規則なのか、規則を作ることが大事でなく、作業効率を上げるための命名規則
- 3分以上真剣に考えてもわからない場合は適当に命名する
- システムの仕様や開発手法は日進月歩なので、永久不滅につかえる命名規則はない
- 規則については定期的に見直しの機会を設けるようにしておく

# DRAFT

下記の命名規則の事例と考え方を参考にして、チームに応じた命名規則を作りたい。

命名の仕方は英語表記にする

```perl
# 日本語のローマ字表記は意外とよみにくい
my $namae = 'nobita';

# 英語が苦手な人は google 翻訳などを活用して英語を調べておく
my $name = 'nobita';
```

慣例的な表現はそのまま採用する

```perl
# 変更前の変数に 1 とつけた
my $name_1 = 'nobita';

# 変更後の変数に 2 とつけた
my $name_2 = join 'nobi_', name_1;

# nobi_nobita (name_2 とは? なんの2番目なのか)
print $name_2;

# 変更前に before とつけるのはよくある表現
my $before_name = 'nobita';

# before とくれば after で完結
my $after_name = join 'nobi_', $before_name;

# nobi_nobita (変数名だけでなにをしたいのかがわかる)
print $after_name;
```

命名の対象を決める

変数名の場合

```perl
# Perl の場合は変数名の前にシジルをつける方法がある
my $address = 'hukuoka-hakata';
my @address = ( 'hukuoka-hakata', 'hukuoka-higashi' );
my %address = ( hukuoka_hakata => 'yoshizuka', hukuoka_higashi => 'tihaya');

# 変数の中身が一つの場合は単数で、配列など複数の場合は複数形を書くように進められることがある
# シジルがついていて配列であることは明白なのにわざわざ複数形をつける意味があるのか?
my @addresses = ( 'hukuoka-hakata', 'hukuoka-higashi' );

# 実際はリファレンスで表現することが多い、この場合は配列かどうかはわからないので名前で表現したとする
my $addresses = ['hukuoka-hakata', 'hukuoka-higashi'];

# ではハッシュのリファレンスのようなデータ構造の場合は?
my $address_hash = { hukuoka_hakata => 'yoshizuka', hukuoka_higashi => 'tihaya'};
my $address_data = { hukuoka_hakata => 'yoshizuka', hukuoka_higashi => 'tihaya'};

# そもそも変数の中身が単数か複数かデータ構造かを名前で表現するのはやりすぎではないだろうか?
# 通常は my で定義しスコープの中で有効の変数を定義するが標準
# 変数を活用したい状況と変数を定義している場所はそう離れていないので、見ればわかるのではないか

# 複数かデータ構造など気にせず単数形で定義するのが現実的な運用
my $address = { hukuoka_hakata => 'yoshizuka', hukuoka_higashi => 'tihaya'};
```

関数名の場合

```perl
# nobita という言葉をくっつける関数
sub nobita {
    my $word = shift;
    my $after_word = 'nobita_' . $word;
    return $after_word;
}

my $name = nobita('nobi');

# 'nobita_nobi'
print $name;

# 関数というのは振る舞いであるので名詞だけで命名するのは無理がある
# いろいろある get_text_with_nobita ? text_join_nobita ? ...
# いろいろアプローチがありすぎてどうしたらいいかわからない。
# 動詞 + 名詞 ということにして、できるだけ短く (加わる + のびた)

sub join_nobita {
    my $word = shift;
    my $after_word = 'nobita_' . $word;
    return $after_word;
}
```

メソッド名の場合

```perl
# join は Perl の標準関数で存在するがメソッド名なら定義可能
package Nobita;

sub new {
    my $class = shift;
    return bless +{}, $class;
}

sub join {
    my $self       = shift;
    my $word       = shift;
    my $after_word = 'nobita_' . $word;
    return $after_word;
}

1;

# どこかのファイルの中で
# メソッド名はそのパッケージ(クラス)のなかで重複しなければよい
my $name = $nobita->join('nobi');

# メソッド名の命名についてはクラス名との兼ね合いも考えなければいけない

```

名前が長い場合はどう省略するのか

名前を複数形にするときに気をつける事

データベースのテーブル名について

コーディングルールを決める時に気をつける事

# SEE ALSO

- <https://www.oreilly.co.jp/books/4873113008/> - Perlベストプラクティス
- <https://www.oreilly.co.jp/books/9784873115658/> - リーダブルコード
