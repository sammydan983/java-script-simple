// src/DNSTunnelingDetector.java

import java.io.*;
import java.nio.file.*;
import java.util.*;
import java.util.stream.Collectors;

public class DNSTunnelingDetector {

    // Calculate Shannon entropy of a string
    public static double shannonEntropy(String s) {
        if (s == null || s.isEmpty()) return 0.0;
        Map<Character, Integer> freq = new HashMap<>();
        for (char c : s.toCharArray()) {
            freq.put(c, freq.getOrDefault(c, 0) + 1);
        }
        double entropy = 0.0;
        int len = s.length();
        for (int count : freq.values()) {
            double p = (double) count / len;
            entropy -= p * (Math.log(p) / Math.log(2));
        }
        return entropy;
    }

    // Compute numeric character ratio
    public static double numericRatio(String s) {
        if (s == null || s.isEmpty()) return 0.0;
        long digits = s.chars().filter(Character::isDigit).count();
        return (double) digits / s.length();
    }

    // Compute heuristic score for a DNS query
    public static int scoreQuery(String qname) {
        String[] labels = qname.split("\\.");
        int maxLabelLen = Arrays.stream(labels).mapToInt(String::length).max().orElse(0);
        double entropy = shannonEntropy(qname);
        double numeric = numericRatio(qname);

        int score = 0;
        if (ma
# java-script-simple
