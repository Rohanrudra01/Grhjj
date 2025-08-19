class Solution {
public:
    int maximumLength(vector<int>& nums) {
        // Count same parity (all odd or all even)
        int oddCount = 0, evenCount = 0;
        for (int num : nums) {
            if (num % 2 == 0) evenCount++;
            else oddCount++;
        }
        int sameParityMax = max(oddCount, evenCount);
        
        // Try longest alternating odd/even pattern (greedy)
        int altLen = 1;
        for (int i = 1; i < nums.size(); ++i) {
            if ((nums[i] + nums[i - 1]) % 2 == 1) {
                altLen++;
            } else {
                altLen = 1;
            }
            sameParityMax = max(sameParityMax, altLen);
        }

        // Try greedy construction of alternating parity subsequence
        int altMax = 1;
        int lastParity = nums[0] % 2;
        for (int i = 1; i < nums.size(); ++i) {
            int currParity = nums[i] % 2;
            if (currParity != lastParity) {
                altMax++;
                lastParity = currParity;
            }
        }

        return max(sameParityMax, altMax);
    }
};
