---
title: 'golang废弃的函数(部分)'
date: 2024-03-29 18:34:55
tags: [Golang]
published: true
hideInList: false
feature: 
isTop: false
---
math.Ceil、math.Floor、math.Round、math.Trunc：这些函数已被 math.RoundTo 替换。
math.Hypot：该函数已被 math.Sqrt 替换。
math.Ilogb：该函数已被 math.Log2 替换。
math.Log1p：该函数已被 math.Log 替换。
math.Pow10：该函数已被 math.Pow 替换。
math.Remquo：该函数已被 math.Modf 替换。
math.Signbit：该函数已被 math.Sign 替换。
math.Sqrt：该函数已被 math.Cbrt 替换。
math.Tanh：该函数已被 math.Sinh 和 math.Cosh 替换。
reflect.DeepEqual：该函数已被 reflect.Equal 替换。
reflect.ValueOf：该函数已被 reflect.Value 替换。
runtime.Caller：该函数已被 runtime.CallerFrame 替换。
runtime.GoroutineID：该函数已被 runtime.GoID 替换。
runtime.NumCPU：该函数已被 runtime.NumCpus 替换。
runtime.Stack：该函数已被 runtime.Callers 替换。
strings.Builder：该函数已被 bytes.Buffer 替换。
strings.Join：该函数已被 strings.Builder.WriteString 替换。
strings.Split：该函数已被 strings.Fields 替换。
strings.Trim：该函数已被 strings.TrimSpace 替换。
testing.T.Errorf：该函数已被 testing.T.Error 替换。
testing.T.Fail：该函数已被 testing.T.Fatal 替换。
testing.T.Log：该函数已被 testing.T.Logf 替换。
time.After：该函数已被 time.NewTimer 替换。
time.Before：该函数已被 time.Since 替换。
time.Now：该函数已被 time.Time 替换。
time.Sleep：该函数已被 time.Until 替换。
