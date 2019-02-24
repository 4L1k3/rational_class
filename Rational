#include <iostream>

int gcd(int a, int b) {
    return b ? gcd(b, a % b) : a;
}

class Rational {
private:
    int n, d;

public:
    Rational(int N = 0, int D = 1) {
        if (D < 0) {
            D = -D;
            N = -N;
        }
        int g = gcd(abs(N), D);
        n = N / g;
        d = D / g;
    }

    Rational operator -() {
        return {-n, d};
    }

    Rational operator +() {
        return {n, d};
    }

    int& numerator() {
        return n;
    }

    int& denominator() {
        return d;
    }

    int numerator() const {
        return n;
    }

    int denominator() const {
        return d;
    }

    Rational& operator++ () {
        n += d;
        return *this;
    }

    Rational operator++ (int) {
        Rational help = *this;
        n += d;
        return help;
    }

    Rational& operator-- () {
        n -= d;
        return *this;
    }

    Rational operator-- (int) {
        Rational help = *this;
        n -= d;
        return help;
    }
};

Rational operator +=(Rational& r1, const Rational& r2) {
    int a1 = r1.numerator();
    int b1 = r1.denominator();
    int a2 = r2.numerator();
    int b2 = r2.denominator();
    r1 = {a1 * b2 + a2 * b1, b1 * b2};
    return r1;
}

Rational operator -=(Rational& r1, const Rational& r2) {
    int a1 = r1.numerator();
    int b1 = r1.denominator();
    int a2 = r2.numerator();
    int b2 = r2.denominator();
    r1 = {a1 * b2 - a2 * b1, b1 * b2};
    return r1;
}

Rational operator *=(Rational& r1, const Rational& r2) {
    int a1 = r1.numerator();
    int b1 = r1.denominator();
    int a2 = r2.numerator();
    int b2 = r2.denominator();
    r1 = {a1 * a2, b1 * b2};
    return r1;
}

Rational operator /=(Rational& r1, const Rational& r2) {
    int a1 = r1.numerator();
    int b1 = r1.denominator();
    int a2 = r2.numerator();
    int b2 = r2.denominator();
    r1 = {a1 * b2, b1 * a2};
    return r1;
}

Rational operator +(const Rational& r1, const Rational& r2) {
    return {r1.numerator() * r2.denominator() + r2.numerator() *
        r1.denominator(), r1.denominator() * r2.denominator()};
}

Rational operator -(const Rational& r1, const Rational& r2) {
    return {r1.numerator() * r2.denominator() - r2.numerator() *
        r1.denominator(), r1.denominator() * r2.denominator()};
}

Rational operator *(const Rational& r1, const Rational& r2) {
    return {r1.numerator() * r2.numerator(), r1.denominator() * r2.denominator()};
}

Rational operator /(const Rational& r1, const Rational& r2) {
    return {r1.numerator() * r2.denominator(), r1.denominator() * r2.numerator()};
}

bool operator == (const Rational& r1, const Rational& r2) {
    return r1.numerator() == r2.numerator() && r1.denominator() == r2.denominator();
}

bool operator != (const Rational& r1, const Rational& r2) {
    return !(r1 == r2);
}
