int largestPalindrome(int n) {
    if( n == 1) {
        return 9;
    }
    int upper = pow(10,n) - 1;
    int lower = pow(10,n-1);
    for( int i = upper; i >= lower; i--) {
        string temp = to_string(i);
        long target = stol(temp + string(temp.rbegin(), temp.rend()));
        for( long j = upper; j * upper >= target; j--) {
            if( target % j == 0) {
                return target % 1337;
            }
        }
    }
    return 9;
}