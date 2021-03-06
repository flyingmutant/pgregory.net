+++
title = "Property based testing"
description = "Preaching of a property-based testing church adept"
date = 2021-03-06T17:26:26+03:00
draft = true
+++

- optimize bug finding given limited time budget for tests
- example vs property
- unit vs integration
- test at the API/abstraction boundary layer (no matter big or small)
- fscheck:
  - “Different paths, same destination” – a diagram that commutes
  - “There and back again” – an invertible function
  - “Some things never change” – an invariant under transformation
  - “The more things change, the more they stay the same” – idempotence
  - “Solve a smaller problem first” – structural induction
  - “Hard to prove, easy to verify”
  - “A test oracle”
- jessica kerr:
  - expect and create failure
  - ask hard questions
  - create visibility you need
  - define success
- math:
  - associative
  - commutative
  - distributive
  - idempotent
  - identity
  - zero
- proper
  - sit back and think
  - start broad and build up
  - assemble multiple properties
- Небольшой список примеров из самых разных областей, удобных для проверки свойств:
  - поле класса должно иметь ранее присвоенное значение (геттеры-сеттеры)
  - в хранилище должна быть возможность прочитать ранее записанный элемент
  - добавление ранее несуществующего элемента в хранилище не затрагивает ранее добавленные элементы
  - во многих словарях не могут храниться несколько разных элементов с одинаковым ключом
  - высота сбалансированного дерева должна быть не больше , где  — число записанных элементов
  - результатом сортировки является список упорядоченных элементов
  - результат кодирования в base64 должен содержать только символы из алфавита base64
  - алгоритм построения маршрута должен возвращать последовательность допустимых перемещений, которая приведет из точки A в точку B
  - для всех точек построенных изолиний должно выполняться
  - алгоритм проверки электронной подписи должен возвращать True, если подпись настоящая и False в противном случае
  - в результате ортонормирования все вектора в базисе должны иметь единичную длину и нулевые взаимные скалярные произведения
  - операции переноса и вращения вектора не должны менять его длину
