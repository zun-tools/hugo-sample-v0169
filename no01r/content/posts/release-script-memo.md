+++
date = '2026-11-13T17:02:54Z'
draft = true
title = 'リリース用の小さな Go ツールを書いた開発メモ'
+++
## 何を作ったか

リリースのたびに手で打っていたバージョン表記の確認を、小さな Go のツールにまとめました。

## 本体

```go
package main

import (
	"fmt"
	"os"
	"regexp"
)

var semver = regexp.MustCompile(`^v\d+\.\d+\.\d+$`)

func main() {
	if len(os.Args) < 2 || !semver.MatchString(os.Args[1]) {
		fmt.Fprintln(os.Stderr, "使い方: release-check v1.2.3")
		os.Exit(1)
	}
	fmt.Println("OK:", os.Args[1])
}
```

## 使い方

```bash
go run . v1.4.0
go run . 1.4.0   # v が無いので失敗する
```

## ひとこと

終了コードで成否を返すようにしたので、CI の途中にそのまま挟めます。
