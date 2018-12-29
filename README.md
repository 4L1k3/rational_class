#include <iostream>
#include <stdio.h>

using namespace std;

const int INF = 1e9, MAXG = 600010, MAXN = 450010;

int n, l, m, b, g, lx, ly, lk, mx, my, mk, a[MAXN], MX;
long long ans, x[MAXG], y[MAXG], k[MAXG], I[MAXG], J[MAXG];

struct tree
{
    int val;
    tree *l, *r;
    tree()
    {
        l = NULL;
        r = NULL;
        val = 0;
    }
};

tree *tr[MAXN];

tree *update(tree *v, int left, int right, int pos)
{
    if (pos >= left && pos < right)
    {
        if (right - left == 1)
        {
            tree *t = new tree();
            t->val = v->val + 1;
            return t;
        }
        if (!v->l)
        {
            v->l = new tree();
            v->r = new tree();
        }
        tree *t = new tree();
        int m = (left + right) / 2;
        t->l = update(v->l, left, m, pos);
        t->r = update(v->r, m, right, pos);
        t->val = t->l->val + t->r->val;
        return t;
    }
    return v;
}
void get_kstat(tree *v1, tree *v2, int left, int right, int k)
{
    if (right - left == 1)
    {
        ans += left;
        return;
    }
    int cntl = v2->l->val - v1->l->val;
    int m = (left + right) / 2;
    if (cntl >= k)
        get_kstat(v1->l, v2->l, left, m, k);
    else
        get_kstat(v1->r, v2->r, m, right, k - cntl);
}

int main()
{
    freopen("gyakkyou.in", "r", stdin);
    freopen("gyakkyou.out", "w", stdout);

    tr[0] = new tree();
    cin >> n >> a[0] >> l >> m;
    MX = a[0];
    for (int i = 1; i < n; i++)
    {
        a[i] = (1LL * a[i - 1] * l + m) % INF;
        MX = max(a[i], MX);
    }
    for (int i = 0; i < n; i++)
    {
        tr[i + 1] = update(tr[i], 0, MX + 1, a[i]);
    }
    cin >> b;
    for (int i = 0; i < b; i++)
    {
        cin >> g >> x[0] >> lx >> mx >> y[0] >> ly >> my >> k[0] >> lk >> mk;
        I[0] = min(x[0], y[0]);
        J[0] = max(x[0], y[0]);
        get_kstat(tr[I[0] - 1], tr[J[0]], 0, MX + 1, k[0]);
        for (int j = 1; j < g; j++)
        {
            x[j] = (((1LL * I[j - 1] - 1) * lx + mx) % n) + 1;
            y[j] = (((1LL * J[j - 1] - 1) * ly + my) % n) + 1;
            I[j] = min(x[j], y[j]);
            J[j] = max(x[j], y[j]);
            k[j] = (((k[j - 1] - 1) * lk * 1LL + mk) % (J[j] - I[j] + 1)) + 1;
            get_kstat(tr[I[j] - 1], tr[J[j]], 0, MX + 1, k[j]);
        }
    }
    cout << ans << endl;
}
